# Node.js

[Node.js](https://nodejs.org) is the JavaScript runtime for this repository. It
runs the web server, along with Remix's tooling for development and testing.

## Why

One major motivation for using Remix is to stick with the web platform instead
of a framework's own version of it (see
[`remix.md`](remix.md#web-platform-first) for details). On the server, that
means web APIs, such as `Request`, `Response`, `URL`, and `FormData`, that
Node.js, Bun, and Deno all provide, so a site's own code rarely touches anything
specific to its runtime.

Anything runtime-specific shows up in only two places:

1. The server entry, which uses `node:http` and `remix/node-fetch-server` to
   connect the runtime's server to `router.fetch()`.

2. The tooling that runs, reloads, and tests the code. In
   [Remix's starter template](https://github.com/remix-run/remix/tree/03c8414c726ea72db832e0f874424976cc2ec647/template),
   TypeScript and JSX run through `node --import remix/node-tsx`, and hot
   reloading comes from `remix/node-hmr`, which uses Node.js module hooks; the
   CLI and test runner are written against Node.js built-in modules too.

So choosing a runtime here mostly means choosing tooling, and Remix's tooling is
built on Node.js.

## Install

pnpm installs Node.js: `pnpm install` installs the version in `engines.runtime`
as the `node` package, links its binary at `node_modules/.bin/node`, and records
its checksum in the lockfile.

Install Node.js only this way, not on its own or globally with pnpm, so that
`engines.runtime` stays the source of truth for the version. Package scripts
already use this copy. To run Node.js directly, use `pnpm exec node`, which
installs first if `node_modules` is missing or out of date.

Any other installation makes the version depend on how and where Node.js runs,
because a bare `node` uses whatever is first on `PATH`:

- A Node.js installed on its own ignores `engines.runtime`.

- A global Node.js from `pnpm runtime set node <version> -g` lands in pnpm's
  global bin directory, which the standalone script added to `PATH` when it
  installed pnpm. Since pnpm 12, inside a project that pins a runtime, as this
  repository does, it runs the pinned version; elsewhere, it runs `<version>`.

With neither, a bare `node` fails with "command not found" instead of running
the wrong version.

## Upgrade

Change the version in `engines.runtime` and run `pnpm install`.
