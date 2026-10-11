# Changelog (fork: Xperia 1 VI, android14-6.1, 6.1.115 only)

Sublevel is fixed at 115 (`os_patch_level=2024-12`, kernel/common
`deprecated/android14-6.1-2024-12` @ `42b45a51b9cf`). A 6.1.176 build broke the
modem despite matching KMI CRCs, so the sublevel never changes.

## repro-r21 (Phase 0): reproduction of Wild r21 6.1.115 KernelSU-Next

Workflow: `.github/workflows/repro.yml` (calls upstream `prepare.yml` unchanged).
Upstream pipeline: WildKernels main `704c5801`; build steps identical to r21's
`660f1cd8` (only `release-from-run` added since).

| Input | Commit | Source |
|---|---|---|
| KernelSU-Next (pershoot dev-susfs) | `4c5853188012f63a1a1fedd4a57fda6375fecb38` | r21 job log |
| SUSFS (simonpunk gki-android14-6.1) | `24743360ea08d98f6ad72b856851abed8de5854f` | r21 job log |
| SUSFS pershoot picks | `88df19e864e9`, `6d4f9a92ac79` | r21 job log + GitLab push events |
| NoMount | `5a610db7649a59eb3e3d710653618d594941f8da` | r21 job log |
| kernel_patches (BBG etc.) | `41ae18b35d20e0c6ac04116785a4a1089528ae94` | r21 job log |
| Droidspaces-OSS | `434d795d80f34852251599cf412841c493aa7177` | r21 job log |
| AnyKernel3 gki-2.0 | `e1e9dce98430c5c6f231f7094a8c7f4ecaf50948` | r21 job log |
| Features | SUSFS+NoMount+BBG+NET+DS+NTSync+Ptrace+Unicode+BPF | r21 job log |
| Branding | `Wild`, unstamped (as r21) | r21 job log |

r21 source: Wild release r21 <- Release From Run 36918415784 <- build run
36828639322, job 110263787688. Log reported KernelSU-Next 33313 / v3.4.0, SUSFS v2.3.0.

Fork changes vs upstream:
- `susfs-setup`: `pins/susfs-pershoot-picks.txt` replaces the run-time
  "newest 2 commits" guess (now it would pick different commits); failed picks are fatal.
- `repro.yml`: pinned dispatch wrapper, includes the NoMount metamodule job.

Config diff vs Wild: pending.
Test result: pending.
