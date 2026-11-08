# oxfmt

[oxfmt](https://oxc.rs/docs/guide/usage/formatter) formats the code and other
text files in this repository. Run `pnpm exec oxfmt` to format them, or
`pnpm exec oxfmt --check` to check them without writing.

## Why

oxfmt comes from Oxc, the same project as oxlint. One tool covers every kind of
file here: TypeScript and JSX, JSON with comments, YAML, and Markdown. It
[takes Prettier's output as its baseline](https://oxc.rs/docs/guide/usage/formatter#prettier-compatible),
so its formatting looks familiar, and it sorts imports itself, where Prettier
needs a plugin.

[Remix formats with oxfmt too](https://github.com/remix-run/remix/blob/remix@3.1.0/oxfmt.config.ts).

## Configuration

`.oxfmtrc.json` sets the formatting options.

oxfmt skips `node_modules`, lockfiles such as `pnpm-lock.yaml`, and the files
that `.gitignore` lists (see
[Ignore files](https://oxc.rs/docs/guide/usage/formatter/ignore-files)).

## Upgrade

Change the version in `devDependencies` and run `pnpm install`. A new version
can format some code differently, so then run `pnpm exec oxfmt` and review what
it changes.

Repoint the links in `.oxfmtrc.json` to the `oxfmt_v<version>` release tag.

oxfmt and oxlint are released together from the same repository, but neither
depends on the other, so their version numbers don't need to match.
