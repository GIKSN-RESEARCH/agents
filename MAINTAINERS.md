# Maintainers

How GIKSN Research projects are run: who can do what, what they owe contributors, and how people move between roles.

## Current maintainers

| Name | GitHub | Role | Areas | Since |
| --- | --- | --- | --- | --- |
| Siddharth Manjul | @SiddharthManjul | Lead maintainer | All | 2026 |

## Roles

| Role | Can | GitHub permission | How it is earned |
| --- | --- | --- | --- |
| Contributor | Open issues and pull requests, claim issues, review | None needed | Anyone |
| Triager | Label, assign, close and reopen issues and pull requests | Triage | Consistent, accurate triage help over at least a month, nominated by a maintainer |
| Reviewer | Approval counts as code owner approval for their areas | Write, listed in CODEOWNERS for those areas | At least 5 substantive merged contributions in the area and 10 useful reviews, nominated by a maintainer |
| Maintainer | Merge, manage releases, run RFCs, moderate | Maintain | At least 3 months as an active reviewer, nominated by a maintainer, no objection from other maintainers within 7 days |
| Lead maintainer | Final decision when consensus fails, owns governance changes | Admin | Founder. Changes through an RFC |

Nominations happen in a private maintainer discussion. The person is asked before anything is announced. Every promotion is announced in Discussions and recorded in this file.

## What maintainers owe contributors

| Duty | Target | How it is tracked |
| --- | --- | --- |
| Triage a new issue | 3 working days | Issues with `needs-triage` older than that are reviewed weekly |
| First response on a ready pull request | 3 working days | Review queue issue, updated automatically every weekday |
| Re-review after the author pushes changes | 2 working days | Review queue |
| Acknowledge a security report | 3 working days | Security advisory timeline |
| Close an RFC's final comment period | 7 days after it opens | RFC status line |
| Credit contributors | Every release | Release notes generated from merged pull requests |

Missing a target is not a failure on its own. Missing it silently is. If a maintainer can't meet a target, they say so on the issue or pull request.

## How to review

### Principles

- Correctness before speed. A fast wrong answer is worse than a slow right one.
- Review the change, not the person. Be specific and explain the why behind every required change.
- Approve when it is good enough to merge, not when it is perfect. Follow-ups can be new issues.

### Every pull request

- [ ] The linked issue is assigned to the author, or the pull request has `small-fix`
- [ ] The scope matches the issue and nothing unrelated is included
- [ ] The title reads well as a changelog line
- [ ] Every required check is green

### Code

- [ ] The behaviour is right, including edge cases and failure paths
- [ ] The tests would fail without the change
- [ ] Public items have docs
- [ ] Every `unsafe` block is necessary, as small as possible and has a convincing `// SAFETY:` comment
- [ ] New dependencies are justified, maintained and appropriately licensed
- [ ] Performance claims come with benchmark output and hardware
- [ ] GPU changes come with pasted GPU test output and hardware

### Research note

- [ ] It answers the question it set out to answer
- [ ] Every claim is sourced, with primary sources where possible
- [ ] The recommendation is clear and follows from the findings

### Experiment

- [ ] It can be rerun from the folder alone
- [ ] `env.txt` is complete
- [ ] The numbers in `README.md` match `results.json`
- [ ] The conclusion doesn't claim more than the data shows. Negative results are welcome

### RFC

- [ ] The motivation is clear and the alternatives are real ones
- [ ] There is a verification plan
- [ ] Open questions are listed
- [ ] The final comment period was announced, and the decision and reason are recorded in the file before merging

### Writing review comments

- Prefix optional suggestions with `nit:`.
- Use "Request changes" only with an explicit list of what must change.
- Use "Approve" with comments when everything remaining is optional.
- Ask questions when you're unsure rather than asserting.

### After the review

- Re-review within 2 working days of the author's update.
- If the author is silent for 14 days after a review, close the pull request with a kind note that it can be reopened.
- Thank first-time contributors in the merge comment.

## Merging

Merge rules, enforced by repository rulesets:

- Every change reaches `main` through a pull request. Nobody, including admins, can push to `main` directly, force-push it or delete it.
- Every required check must pass. Nobody can bypass checks.
- Squash merge only. The pull request title becomes the commit message.
- Contributor pull requests need approval from a code owner, given after the last push. All review threads must be resolved.
- **While there is only one maintainer,** the lead maintainer can merge their own pull requests without a second approval. This goes through the ruleset's audited pull-request bypass, so each one is logged. Checks still apply. **When a second maintainer joins, this bypass is removed** and every pull request needs approval from someone other than its author.

## Triage

1. New issues arrive with `needs-triage`.
2. A triager or maintainer reads it. They reproduce bugs, ask for missing details and add one `area/` label.
3. They decide one of:
   - **Claimable:** add `help wanted`, or `good first issue` if it meets the bar below. Remove `needs-triage`.
   - **Maintainer work:** remove `needs-triage` and assign it.
   - **Needs a design first:** add `needs-rfc`.
   - **Won't do:** close it with a one-line reason.
4. `blocked` is added with a link to the blocking issue, and removed when that lands.

**Labels are applied by people only.** Automation never adds or removes labels, apart from the default labels set by issue forms.

### The bar for `good first issue`

A good first issue:

- names the files to change and the test that proves it's done
- needs no design decisions
- is likely under about 200 changed lines
- has a maintainer ready to answer questions on it

If it fails any of these, it is `help wanted` instead.

## Decisions

- **Day-to-day:** lazy consensus. A maintainer proposes, and silence for 3 working days means agreement.
- **Public APIs, file formats and architecture:** the RFC process in CONTRIBUTING.md.
- **Disagreement:** argued in the open on the issue or RFC. If maintainers can't agree, the lead maintainer decides and writes down why.
- **Governance changes:** an RFC in the `.github` repository.

## Code of Conduct enforcement

Reports go to <contact-email> and are seen only by maintainers who are not involved. The reporter's identity is kept confidential.

Maintainers follow the Contributor Covenant enforcement ladder:

| Step | When | Action |
| --- | --- | --- |
| 1. Correction | Inappropriate language or unwelcome behaviour | Private written note explaining the problem. A public apology may be requested |
| 2. Warning | A single serious incident or repeated minor ones | Written warning with consequences for continuing. No interaction with the people involved for a set period |
| 3. Temporary ban | Serious or sustained violation | Blocked from the org for a set period using GitHub's org block, plus interaction limits on affected repositories |
| 4. Permanent ban | A pattern of violations, harassment or aggression | Permanent org block |

Moderators can also hide comments, lock heated threads and set temporary interaction limits while a report is handled. Every enforcement action is logged privately with the date, the step and the reason. Maintainers involved in a report step aside from deciding it.

## Security response

Reports come in through GitHub private vulnerability reporting or <contact-email>.

| Stage | Target |
| --- | --- |
| Acknowledge the reporter | 3 working days |
| Confirm and assess severity | 7 days |
| Fix released and advisory published | 90 days, sooner for critical issues |

Fixes are developed in a private security advisory fork. Advisories are published through GitHub Security Advisories, with a CVE requested where it applies. Reporters are credited unless they ask not to be.

## Releases

Projects are pre-1.0 and may break APIs between minor versions. A release is a maintainer-merged pull request that bumps versions and updates the changelog. Release tags (`v*`) are protected and can only be created by maintainers. Every changelog credits the contributors in it.

## Account security

- Two-factor authentication is required for every org member.
- Maintainers sign in with a security key or authenticator app, not SMS.
- Secrets live only in GitHub encrypted secrets, never in a repository.
- Workflow tokens default to read-only. Workflows from first-time contributors need a maintainer's approval before they run.

## Stepping down

- A maintainer inactive for 6 months moves to emeritus. Their write access is removed and they stay credited below. They can return by asking.
- A maintainer can step down at any time by opening a pull request to this file.
- A maintainer who seriously breaches the Code of Conduct or abuses their access is removed by the lead maintainer, with the reason recorded privately.

## Conflicts of interest

Maintainers disclose any employer or financial interest in a change they review. Once there are two or more maintainers, a maintainer does not approve a change that mainly benefits their employer without a second maintainer's approval.

## Emeritus

None yet.
