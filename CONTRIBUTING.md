# Contributing to GIKSN Research

This is the contribution policy for every Open Build AI repository. Each repository adds its own `CONTRIBUTING.md` with its layout and commands.

Every rule here is either checked automatically on your pull request or owned by a named maintainer role with a public response target. The table at the end shows which.

## Four kinds of contribution

| Kind | Where it goes | How it starts | Done when |
| --- | --- | --- | --- |
| Research note | `research/notes/` | An issue using the research note form | It answers its question, every claim is sourced, and it is approved |
| Experiment | `research/experiments/` | An issue using the experiment form | Someone else could rerun it from what is in the folder. Negative results are merged too |
| RFC (design) | `rfcs/` | An issue using the RFC form, then a pull request adding the RFC | The comment period has closed and the decision is written at the top |
| Code | `crates/` | An issue | All checks pass and a code owner has approved it |

## The workflow

### 1. Find an issue

Issues open for contributors carry `help wanted` or `good first issue`. `good first issue` is reserved for people who have not had a pull request merged in that repository yet. Issues with `no-gpu-needed` can be done on any machine.

If what you want to do has no issue, open one using the matching form and wait for a maintainer to triage it.

### 2. Claim it

Comment `/claim` on the issue. A bot assigns it to you if:

- it is open, unassigned, not `blocked` and labelled `help wanted` or `good first issue`
- you have fewer than 2 open issues assigned in that repository
- for `good first issue`, you have no merged pull requests in that repository yet

Comment `/unclaim` to release it.

A claim lasts while you are active. After 7 days with no comment or linked pull request from you, the bot posts a reminder. After 3 more days, it releases the issue. You can claim it again.

### 3. Open a pull request

- **Link the issue in the description**, for example `Closes #12`. The issue must be assigned to you.
- **Fill in every section of the template.** "How it was tested" is required.
- **Title:** Conventional Commits: `feat:`, `fix:`, `docs:`, `research:`, `rfc:`, `test:`, `refactor:`, `perf:` or `chore:`, followed by a short summary. We squash-merge, so the title becomes the commit message and the changelog line.
- **Sign off every commit** (see Sign-off below).
- **Keep it to one change.** Unrelated fixes go in their own pull request.
- **Mark it ready.** Open it as a draft while you work, then mark it ready for review. Review-time targets start when it is ready.

Exception: a maintainer can exempt a trivial fix (a typo, a broken link) from the issue rule by adding the `small-fix` label.

### 4. Review

A code owner reviews every pull request. Expect a first response within 3 working days of it being ready. That target is tracked automatically: pull requests that miss it are listed publicly on the repository's **Review queue** issue.

Reply to review comments, push fixes as new commits (don't force-push during review) and re-request review when you're done. Approvals are dismissed when new commits arrive.

If you go 14 days without responding to a review, a maintainer may close the pull request. You can reopen it when you're back.

## RFCs

1. Open an issue with the RFC form to check the idea is wanted.
2. Copy `rfcs/0000-template.md` to `rfcs/NNNN-short-title.md`, using the next free number, and open a pull request. Status: `Draft`.
3. When you say it is ready, a maintainer sets the status to `Final comment period` and announces it. Comments stay open for 7 days.
4. A maintainer sets `Accepted` or `Rejected`, fills in the `Decision` line with the reason and merges it either way. Rejected RFCs are kept on purpose.

Anything that changes a public API, a file format or the architecture needs an accepted RFC before code.

## Research standards

**Notes** need the sections Question, Findings, Sources and What this means for us. Sources must link to the material. Primary sources (papers, source code, official docs) beat blog posts.

**Experiments** need a folder containing:

- `README.md` with Question, Method, Result, What it means and How to rerun
- the script or notebook that produced the result
- `results.json` with the raw numbers, whose `experiment` field matches the folder name
- `env.txt` with the hardware, OS, toolchain and library versions

If it ran on Kaggle, link the exact notebook version and commit an exported copy with outputs under 1 MB. A number nobody can reproduce will not be merged.

The `research` check validates all of this on every pull request.

## Code standards

- Formatting and lints: `cargo fmt --all` and `cargo clippy --workspace --all-targets -- -D warnings` must be clean.
- Tests: new behaviour comes with tests, including failure paths.
- Unsafe code: allowed only in crates explicitly marked for it. Every `unsafe` block needs a `// SAFETY:` comment explaining why it is sound.
- Dependencies: a new dependency needs a reason in the pull request description. Licences, security advisories and sources are checked automatically.
- Performance: claims need benchmark output and the hardware in the pull request.
- GPU: CI has no GPU. GPU tests sit behind the `gpu` feature. If your change touches the GPU, paste the GPU test output and hardware into the pull request, or ask a maintainer to run them.

## AI tools

You can use AI tools. You are responsible for every line you submit: you must understand it, have run it and be able to answer review questions about it. Pull requests that look generated and unreviewed are closed without detailed review.

## Sign-off

We use the [Developer Certificate of Origin](https://developercertificate.org/) instead of a CLA. Every commit needs a `Signed-off-by` line whose email matches the commit author:

```bash
git commit -s -m "fix: handle empty prompts"
```

Forgot? Fix the whole branch with `git rebase --signoff main` and push. This is the one case where force-pushing your branch is fine.

## Licence

Unless you explicitly state otherwise, any contribution you intentionally submit for inclusion in the work, as defined in the Apache-2.0 licence, shall be dual licensed as MIT OR Apache-2.0, without any additional terms or conditions.

## How each rule is enforced

| Rule | Enforced by |
| --- | --- |
| Conventional Commits title | `title` check (required) |
| Every commit signed off | `dco` check (required) |
| Pull request linked to an issue assigned to you | `policy` check (required) |
| "How it was tested" filled in | `policy` check (required) |
| Formatting, lints, tests and docs | `fmt`, `clippy`, `test` and `docs` checks (required) |
| Builds on the minimum supported Rust version | `msrv` check (required) |
| Dependency licences, advisories and sources | `deny` check (required) |
| Unsafe code only where allowed, always documented | `unsafe-scope` check and the `undocumented_unsafe_blocks` lint (required) |
| Research note, experiment and RFC format | `research` check (required) |
| Code owner approval | Branch ruleset and CODEOWNERS |
| No direct or force pushes to `main` | Branch ruleset, no exceptions |
| Claim rules and expiry | `/claim` bot and the daily stale-claim sweep |
| Maintainer response time | Review queue, updated every weekday |
| Code of Conduct | Maintainers, using the enforcement ladder in `MAINTAINERS.md` |

## Talking

Use GitHub Discussions for questions and design conversation. Decisions are made and recorded on GitHub: in issues, RFCs and pull requests.
