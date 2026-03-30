Objective: Fix the week 2 notebook's failing NVIDIA-backed `inspect_ai` run by identifying the root cause and preventing the same misconfiguration from reaching `eval()`.

Plan:
- [x] Inspect the failing eval log and notebook state to identify the root cause.
- [x] Confirm how `inspect_ai` parses `openai-api/<service>/<model>` names.
- [x] Patch the notebook to validate model specs before evaluation and surface the active config.
- [x] Verify the notebook content reflects the fix and matches the failing-log diagnosis.

Verification:
- Direct notebook-content checks confirming the validation helper and corrected NVIDIA example.
- Direct execution of the notebook config cell confirming the validator rejects `openai-api/nvidia/qwen2.5-7b-instruct`.
- Direct log-header checks showing later runs with `openai-api/nvidia/qwen/qwen2.5-7b-instruct` completed successfully.

Review:
- Root cause: the failing run used `openai-api/nvidia/qwen2.5-7b-instruct`, which omits the provider namespace expected by NVIDIA's catalog, and the live kernel state had drifted from the saved notebook.
