## Gotchas

- Missing markers: The script requires `<!-- devplan:start -->` and `<!-- devplan:end -->`. Without them, it aborts.
- Phase detection: Only headings that exactly match `## Phase: <Title>` are recognized.
- Empty phases: If a phase has no checkbox tasks, a placeholder `- [ ] (no tasks listed)` is inserted.
- Closed issues: By default, closed issues are not updated. Use `--update-closed` if you need to sync them.
- Labels: If the configured label does not exist, the script attempts to create it; this may require permissions.
- `jq` dependency: JSON parsing of `gh` output requires `jq`.
- Rate limits: Bulk updates may hit GitHub rate limits; re-run after a cooldown.


