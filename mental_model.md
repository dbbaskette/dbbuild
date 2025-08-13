## Mental Model

`dbplan` turns a structured dev plan into GitHub issues. The plan lives in `DEVPLAN.md` (preferred) or `PROJECT.md` inside a demarcated section:

```
<!-- devplan:start -->
... plan content ...
<!-- devplan:end -->
```

- One phase maps to one GitHub issue titled `Feature: <Phase>`.
- Phase tasks remain as a single checklist in the issue body.
- A hidden marker binds the issue to its phase for idempotent updates.
- The target repository is inferred from the current git remote using `gh`.

Key properties:

- Deterministic: re-running with unchanged plan yields no changes.
- Additive: never deletes issues; only creates or updates.
- Safe defaults: skips closed issues unless explicitly allowed.


