# jasoncookdesign.github.io

Static HTML on GitHub Pages. No build step. Merging to main deploys to jasoncookdesign.com immediately.

- Preview: `python3 -m http.server 8000` from the repo root, then check changed pages in a browser.
- `blog/` is generated output. Never hand-edit it. Edit `content/blog/*.md` or `templates/blog/`, regenerate, commit both.
- Add a case study by copying the latest `csNN.html` and linking it from `index.html`.
- Branch from main, push the branch to this repo, open a PR. Ignore the README's fork instructions.
- Claude may merge its own PRs. Exception: any PR that touches `.claude/` or `.github/` is merged by the owner. This exception is a convention, not enforced by settings.
- Roll back a bad deploy with a `revert:` PR, then merge it.

## TDD exception (recorded ruling)
Markup, style, and content changes have no test runner here, so they are a standing exception to the TDD discipline. State the exception in each PR description. The blog generator and any JS or Python logic get full TDD.
