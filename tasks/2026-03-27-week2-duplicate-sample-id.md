Objective

Fix the `inspect_ai` week 2 notebook failure:
`The dataset contains duplicate sample ids ...`

Plan

- [x] Inspect the notebook cells that construct the MMLU dataset.
- [x] Confirm root cause in local `inspect_ai` behavior and notebook code.
- [x] Patch the notebook to preserve or generate unique sample ids.
- [x] Run a direct execution check for dataset id uniqueness.
- [x] Review the resulting diff and note residual risk.

Verification

- Load the patched dataset construction path in the local virtualenv.
- Check sample count against unique id count.
- Confirm there are no duplicate ids in the constructed dataset.

Results

- Reproduced the failure mode with the cached MMLU dataset and the notebook's custom `record_to_sample` function.
- Without `auto_id`, all 14,042 samples had `id=None`, yielding only 1 unique id value.
- With `auto_id=True`, the same 14,042 samples had 14,042 unique ids, starting with `[1, 2, 3]`.

Review

- Prefer the smallest notebook change that preserves tutorial intent.
- Avoid unrelated edits in the dirty worktree.
- `w2/inspect_ai_tutorial_week_2.ipynb` is currently untracked, so there is no diff against `HEAD`; review was against the edited working copy only.
