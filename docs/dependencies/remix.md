# Remix

[Remix](https://remix.run) is a full-stack web framework. This repository uses
Remix 3. Unlike earlier versions, Remix 3 doesn't use React; it has its own
component model (`remix/component`).

## Why

I chose Remix for two reasons: how it works and what it includes.

### Web platform first

What I learn using Remix is mostly the web platform, not a framework's own
version of it. For example:

- The router is a fetch handler: a `Request` goes in and a `Response` comes out.

- Forms are plain HTML forms that work without JavaScript.

- When a component handles an event, it gets the browser's own event, not a
  wrapper like React's synthetic events.

The closest alternative is React Router v7 and later, which continues Remix v2
with React. Both come from the same team and put the web platform first. React
Router shares the first two, but not the third: the component gets React's
synthetic event.

Remix still adds its own layer for UI. Components are written in JSX, which
isn't a web standard. Rendering, hydration, and `handle.update()` are Remix's.
That layer is thin, though. Pages are server-rendered HTML, and only components
marked with `clientEntry` hydrate in the browser.

### One package

Remix covers most of what a site needs in one package, from sessions and login
to validation, data, and tests. In
[Remix's words](https://github.com/remix-run/remix/blob/03c8414c726ea72db832e0f874424976cc2ec647/packages/remix/guides/01-start-here.md?plain=1#L8),
"for most web apps, `remix` can be the only runtime dependency in
`package.json`."

For me, that keeps upgrades simple: instead of a separate version for each of
many packages, there's one `remix` version to change.

React stacks typically spread across several packages that have to move
together, such as `react`, `react-dom`, and the framework's own packages. An app
still needs separate libraries for login, validation, and data.

The flip side is giving up React's ecosystem, such as its component libraries.
However, with AI agents doing most of the coding today, rebuilding components is
an acceptable cost.
