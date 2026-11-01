# site-shell

This is a Remix 3 outer shell for my sites. Each site keeps its own repository
and sits inside a copy of this shell to form a complete Remix project.

## Setup

This repository uses Node.js as the JavaScript runtime and pnpm as the package
manager. Node.js is installed via pnpm like any other package, so pnpm becomes
the only thing to install by hand (see
[`docs/dependencies/pnpm.md`](docs/dependencies/pnpm.md#why) for details).

Install pnpm with the
[standalone script](https://pnpm.io/installation#using-a-standalone-script),
which doesn't need Node.js, then run `pnpm install`.

## License

MIT. See [`LICENSE`](LICENSE).
