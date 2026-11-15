# Site

Each site keeps its own repository and is mounted in the root-level `site`
directory of a copy of this repository.

## Repository nesting

This repository's `.gitignore` uses `/site/` to ignore the root-level `site`
directory, keeping this repository from recording a site's files or commits.

Git allows a repository inside another repository, so the ignore rule is not
what makes the nested repository legal. However, leaving the root-level `site`
directory unignored records a gitlink instead:

- `git add site` stores a gitlink, mode `160000`, and Git warns that a clone
  will not contain the site's files and will not know how to obtain them.

- `git submodule add <url> site` stores that same gitlink plus a `.gitmodules`
  entry with the site's URL, so a clone can fetch one chosen commit. This
  repository is copied once per site and does not bind to a commit of any site.
