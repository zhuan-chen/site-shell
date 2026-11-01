# pnpm

[pnpm](https://pnpm.io) is the package manager for this repository.

## Why

I chose pnpm because of how I organize my sites. This repository is an outer
shell, and each site forms its own project within a copy of it, so a machine
with several sites has several `node_modules` holding mostly the same packages.
pnpm keeps each package version once in a global store and links it into each
project. npm, in contrast, copies the full tree into every project, so each new
site takes another full copy's worth of disk space.

pnpm also manages Node.js, installing the version in the `engines.runtime` field
of `package.json`, as [`nodejs.md`](nodejs.md#install) explains. npm can't: it
ignores `engines.runtime`, and it only checks `devEngines.runtime`, failing on a
mismatch instead of downloading the right version. With pnpm, the Node.js
version is pinned like every other dependency, and with that, pnpm becomes the
only thing to install before working on this repository.

## Install

Install pnpm with the
[standalone script](https://pnpm.io/installation#using-a-standalone-script),
then run `pnpm install`. The standalone script doesn't need Node.js, which pnpm
installs afterward. Other ways, such as npm or Corepack, need a Node.js
installed on its own, which [`nodejs.md`](nodejs.md#install) rules out.

The repository decides which version of pnpm runs: the version is recorded in
`packageManager`, with its checksums in the lockfile, and pnpm 10 and later
switch to it by default, downloading it if needed.

## Upgrade

Change the version in `packageManager`, and the next pnpm command downloads and
runs it, updating its checksums in the lockfile.
