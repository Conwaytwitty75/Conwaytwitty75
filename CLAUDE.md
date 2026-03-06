# CLAUDE.md

## Repository Overview

This is a **GitHub profile repository** — the special `Conwaytwitty75/Conwaytwitty75` repository whose `README.md` is automatically displayed on the GitHub profile page at `https://github.com/Conwaytwitty75`.

This is not a software project. There is no application code, build system, test suite, or dependency management. The sole purpose of this repository is to maintain the public-facing GitHub profile README.

## Repository Structure

```
Conwaytwitty75/
└── README.md    # GitHub profile README (rendered on the profile page)
```

## Key File

### `README.md`
- Rendered directly on the GitHub profile at `https://github.com/Conwaytwitty75`
- Supports standard GitHub Flavored Markdown (GFM)
- Supports HTML, badges, images, and embedded content that GitHub allows
- Currently contains only the default boilerplate template with placeholder comments

## Development Conventions

### Editing the Profile README
- Edit only `README.md` for profile content changes
- Keep markdown valid and well-structured
- Images and assets should be hosted externally (e.g., GitHub raw URLs, shields.io, or other CDNs) since this repo has no asset pipeline
- Badges can be generated via [shields.io](https://shields.io) or [img.shields.io](https://img.shields.io)

### Commit Style
- Use clear, descriptive commit messages in present tense (e.g., `Update README with project links`)
- Since there is only one meaningful file, commits will almost always touch only `README.md`

### Branches
- `main` / `master`: primary branch, reflects the live profile
- `claude/*`: branches used by AI-assisted workflows

### No Build, Test, or Lint Steps
There are no scripts, build commands, test runners, or linters configured. No `npm install`, `make`, or other setup steps are needed.

## What AI Assistants Should Know

- **Do not create application code** unless explicitly asked to turn this into a software project
- **Do not add package.json, requirements.txt, or other dependency files** without explicit instruction
- **README.md content** is public-facing and appears on the GitHub profile — keep it professional and accurate
- **No CI/CD** is configured; changes go live when pushed to the default branch (`main`)
- **The entire codebase is one file**: all meaningful changes happen in `README.md`

## Useful GitHub Profile README Resources

- [GitHub profile README docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme)
- [shields.io](https://shields.io) — badges for languages, build status, etc.
- [github-readme-stats](https://github.com/anuraghazra/github-readme-stats) — dynamic stats cards
- [GitHub Flavored Markdown spec](https://github.github.com/gfm/)
