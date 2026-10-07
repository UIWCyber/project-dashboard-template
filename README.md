# Project dashboard template

A template for team software projects. It gives your team a dashboard that tracks your work
layer by layer across your software stack, shows which pull requests are ready, lists failed
build tests, and counts commits by team member.

**Start here: open [`dashboard/guide.html`](dashboard/guide.html)** (the student guide) in your
browser, or read it on your published dashboard at `guide.html`.

## Quick start

1. Press **Use this template** to create your team repository.
2. Edit `dashboard.config.json`: your project, your team members, and your layers. Every layer
   names a `stack_tier` (presentation, application, integration, data, security, platform,
   delivery, quality or observability).
3. Check it: `python3 scripts/generate_dashboard.py --check` (Windows: `py` instead of `python3`).
4. Commit and push. The **Labels sync** workflow creates your `layer:` labels.
5. Turn on GitHub Pages with Source **GitHub Actions**, then run **Dashboard refresh** from the
   Actions tab.

## Build it on your computer

| | macOS or Linux | Windows |
| --- | --- | --- |
| From your repository | `bash refresh.sh` | `powershell -ExecutionPolicy Bypass -File refresh.ps1` |
| With sample data | `bash refresh.sh --demo` | `powershell -ExecutionPolicy Bypass -File refresh.ps1 -Demo` |

Then open `_site/index.html`. You need Python 3.9 or later and, for real data, the GitHub CLI
signed in with `gh auth login`.

## Workflows

| Workflow | When | What |
| --- | --- | --- |
| Dashboard refresh | every 6 hours, on push to main, on demand | rebuilds and publishes the dashboard |
| Build tests | every pull request and push to main | validates the config, runs each layer's tests; require `all-green` |
| Layer label check | pull request opened or relabeled | fails until the PR has a `layer:` label |
| Labels sync | config changes on main | creates or updates labels |
| Local scripts | changes to the refresh scripts | runs `refresh.sh` on Linux and `refresh.ps1` on Windows |

The template's own scripts use only the Python standard library.
