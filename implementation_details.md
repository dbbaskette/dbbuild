## Implementation Details

Parsing:

- Extract the plan section using the markers `<!-- devplan:start -->` and `<!-- devplan:end -->` with `awk`.
- Recognize phases by headings matching `## Phase: <Title>`.
- Collect checkbox lines under each phase matching `- [ ]` or `- [x]`.

Issue binding:

- Build a stable `phase-id` as a short hash of `<plan file path>:<phase title>`.
- Include a hidden HTML comment marker in the body: `<!-- plan-source: <file>; phase-id: <hash> -->`.
- Search for existing issues by marker (in:body) first, fallback to exact title.

GitHub operations:

- Infer repository via `gh repo view -q .nameWithOwner`.
- Ensure the label exists (`gh label list` / `gh label create`).
- Create: `gh issue create --title "Feature: <Phase>" --label <label> --body-file <file>`.
- Update: `gh issue edit <number> --body-file <file>`; ensure label present.

CLI options:

- `--file`, `--label`, `--repo`, `--dry-run`, `--update-closed`, `--verbose`.

Idempotency:

- Compare normalized bodies before editing to avoid needless updates.
- Skip closed issues unless `--update-closed`.

Dependencies:

- `git`, `gh`, `jq`, and standard POSIX tools (`awk`, `sed`, `grep`).

Branch mode:

- `--branch [ISSUE_NUMBER]` lists open issues labeled with the configured label and whose titles start with `Feature:`.
- User selects from a menu or passes the issue number to skip prompting.
- Branch name format: `feature/issue-<number>-<slugified-title>`.
- Creates local branch if needed, checks it out, and pushes to `origin` with upstream tracking.


