# oxlint

[oxlint](https://oxc.rs/docs/guide/usage/linter) lints the code in this
repository and checks its types. Run `pnpm exec oxlint`.

## Why

The code runs without a type check: `remix/node-tsx` removes the types as
Node.js loads each file,
[without checking them](https://github.com/remix-run/remix/blob/03c8414c726ea72db832e0f874424976cc2ec647/packages/node-tsx/README.md?plain=1#L7),
and Remix's test runner does the same. Yet Remix's types catch real mistakes.
For example, after a route pattern renames a parameter,
[calls that still pass the old name](https://github.com/remix-run/remix/blob/03c8414c726ea72db832e0f874424976cc2ec647/packages/remix/guides/02-routing-and-controllers.md?plain=1#L40)
fail to type-check. So Remix's testing guide
[keeps type checking as a separate command](https://github.com/remix-run/remix/blob/03c8414c726ea72db832e0f874424976cc2ec647/packages/remix/guides/13-testing.md?plain=1#L443).

oxlint runs that check through `oxlint-tsgolint`, which is built on
[typescript-go](https://github.com/microsoft/typescript-go), the Go code behind
TypeScript 7. Its errors are TypeScript's own, with the same codes as `tsc`, so
this repository doesn't need the `typescript` package.

[Remix lints with oxlint too](https://github.com/remix-run/remix/blob/03c8414c726ea72db832e0f874424976cc2ec647/.oxlintrc.json).

The common alternatives fall short:

- ESLint reads TypeScript through `typescript-eslint`, which needs TypeScript's
  JavaScript API. TypeScript 7 no longer has one, and `typescript-eslint` 8.72.1
  supports only TypeScript below 6.1.

- [Biome](https://biomejs.dev) also works without TypeScript, but it can't
  report type errors, and its type-aware rules rely on its own type inference
  rather than TypeScript's.

## Configuration

- `.oxlintrc.json` turns on the type-aware rules and type checking, and makes
  warnings fail the run.

- `tsconfig.json` holds the TypeScript options that the checker and Remix's
  tools read.

## Upgrade

Upgrade `oxlint` and `oxlint-tsgolint` together. Their version numbers aren't
related, but `oxlint` names the lowest `oxlint-tsgolint` version it works with
as a peer dependency, and raises it from time to time. To see it for a new
version, run `pnpm view oxlint@<version> peerDependencies`.

To upgrade, change both versions in `devDependencies`, keeping `oxlint-tsgolint`
at or above that minimum, and run `pnpm install`. With `strictPeerDependencies`
in `pnpm-workspace.yaml`, that install fails if `oxlint-tsgolint` is too old.
Only that install fails, though, so run `pnpm peers check` to check again later.

The TypeScript that checks the code comes with `oxlint-tsgolint`, so upgrading
it can upgrade TypeScript too. A new TypeScript major version can remove options
or change their defaults, so read its release notes first. `@types/node` follows
the Node.js version instead (see [`nodejs.md`](nodejs.md#upgrade)).
