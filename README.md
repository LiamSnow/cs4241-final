# CS 4241 Final Project

[Hosted Link](https://final.tempel-alpha.ts.net)

[Proposal](PROPOSAL.md)

TODO [Video Link](https://)

## Team
TODO add roles
 - Liam Snow
 - Jake Olsen
 - Ben Tyler
 - Ryan Wright

## Description
TODO (2 paragraphs)

## Technology
This project has a core focus around server side rendering (SSR)
and CRUD. Everything on the client side is handled by HTMX
which means there is zero client side Javascript, while still
being a reactive fast webapp.

This webapp was built using the following technologies:
 - [Express.js](https://expressjs.com): web/server framework
 - [Handlebars](https://handlebarsjs.com/): HTML templating
 - [daisyUI](https://daisyui.com/) (tailwind): UI components
 - [HTMX](https://daisyui.com/): javascript behavior in HTML attributes
 - [SQLite](https://www.sqlite.org/): lightweight file-based database
 - __Self Hosted__: hosted on Arch Linux server with Docker and Tailscale (see [Hosting](#hosting))

### Achievements
 - Secure storage of user credentials using hashing with salting
 - Protected endpoints: even with the `locationID` of another users location, it cannot be viewed
 - Protected database calls: users can only view, create, edit, or delete locations and foods for their account (this is checked at every database call)
 - Seamless HTML injection (no page reload): whenever a food is added or edited, a POST request is made which returns new HTML (only inside `<body>`), which HTMX replaces with the current body content

### Challenges
 1. The biggest challenge we faced in this project was using SvelteKit. We had many attempts at it, but eventually decided that doing this project without a front-end framework (SSR) was more feasible.
 2. Another challenge we faced with this project was how to make the edit food dialog/modal. Every other dialog in this app gets generated at page load. In order to solve this we used some more advaned HTMX features. When the edit food button is pressed it fetches the api `/location/{locationID}/edit-food-dialog/{foodID}` and injects the response (HTML for dialog) into a div at the bottom of the page. Whenever that div is changed (`hx-on::after-swap`) it opens the modal.

## Development
```bash
npm run server # to view website (hosted at `http://localhost:3000`)
npm run tailwind # to live reload css
```

## Hosting

This project was self hosted on an Arch Linux
server with Docker and Tailscale.

__Example Docker Compose__ (tailscale removed):
```yaml
name: final
services:
  final:
    container_name: final
    image: node:latest
    volumes: [.:/app]
    working_dir: /app
    command: sh -c "npm install && npm start"
    restart: unless-stopped
```

__`.env` File__:
```bash
NODE_ENV=production
```


