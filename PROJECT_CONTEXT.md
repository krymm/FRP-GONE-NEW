# FRP GONE — Project Context and Handoff

Updated: October 15, 2026, 11:33 AM CST (Regina, Saskatchewan)
Repository: `krymm/FRP-GONE-NEW`; branch: `master`
Reviewed base: `c41b8921ff0563a8033a0120b54bf27499be334c`
Local project root: `X:\FRP-GONE\`
Working tree: Unknown; review used remote repository access.
Status: Dependency scaffold with restored submodule URL mappings; integrated application and runtime remain unverified.

## Goal and constraints

Build a Windows phone-servicing toolkit with an interactive menu, model-specific configuration or launchers, supporting tools, programmer collections, setup documentation, and consistent logging. Historical scope focused on FRP-related servicing using Qualcomm tooling; MediaTek support was also discussed. Intended flow: menu → model configuration → shared launcher → selected dependency. This integration is planned, not established by dependency presence.

Use GitHub and web search for sourcing, not Firecrawl or Hugging Face. Preserve `X:\FRP-GONE\` as the intended local root and allow additional models without duplicating the implementation. Establish authorized servicing scope before implementing device-changing functions.

## Current implementation

The parent contains `PROJECT_CONTEXT.md`, `_firehose_list.txt`, four submodule gitlinks, and ancillary directories under `current_session_context/`, `pip/cache/`, and `Microsoft/Windows/PowerShell/`. Directory listings were inspected; artifact contents were not comprehensively audited.

This revision adds root `.gitmodules` with explicit HTTPS URLs for all four existing gitlinks. It does not change dependency commits, upstream source, programmer binaries, or device behavior. No branch-tracking entries are added. The parent records pinned commits; do not use `git submodule update --remote` as a substitute for reproducing them.

The reviewed base has no root README, SKILL.md, project-level menu/setup script, models directory, tests, or CI configuration. Their absence at the root does not prove there are no relevant local untracked files or scripts buried in artifact directories. The intended menu, shared launcher, model wrappers, setup flow, and project skill remain unverified/planned. Keep this existing handoff as the canonical context file rather than introducing a duplicate SKILL.md.

## Submodule references

| Parent path | Upstream repository | Pinned commit |
|---|---|---|
| `edl` | `https://github.com/bkerler/edl.git` | `1cda1a616748d608667b2d13b73a28d3197ceb45` |
| `firehoses` | `https://github.com/zenlty/Qualcomm-Firehose.git` | `c9cfcae6ec62f2586aaeb96d9a99b59eb0b10e27` |
| `firehoses-pixel-oneplus` | `https://github.com/thantoeaungat/firehose.git` | `56bd8a3d54f9dc69ddf59ee486c557b8cb25cd05` |
| `mtk` | `https://github.com/bkerler/mtkclient.git` | `7cb40e727727dfe3faa065eefb29b16ed29bbdf1` |

All four entries were individually confirmed as submodules during the remote review. The EDL and MediaTek source commits were inspected in their upstream repositories; the two collection commit identities were subsequently verified against their listed upstreams. These checks do not verify programmer compatibility, binary safety, redistribution rights, or hardware behavior.

EDL itself declares `Loaders` in its `.gitmodules`, with URL `https://github.com/bkerler/Loaders` and branch metadata `main`. At the pinned EDL revision, `Loaders` is a gitlink pinned to `6c416255056a178f54ccd7ee9b67d04a5bdfa8e6`. Recursive initialization is required to populate it. Ordinary pinned checkout does not require advancing to that branch's latest commit.

## Code map

- `edl/edl.py`: inspected upstream CLI/orchestration entry point. Uses docopt, USB/serial transport, Sahara communication, and Firehose/streaming clients. Main orchestration is in `main.run()`.
- `edl/edlclient/Library/`: referenced transport and protocol implementations; not exhaustively reviewed.
- `edl/pyproject.toml`: inspected manifest declares edlclient 3.62, Python >=3.10, and installed console entry point `edlclient.edl:run`. Installed-console behavior was not tested.
- `mtk/mtk.py`: inspected upstream argparse entry point, banner version 2.1.4; delegates to `Main(args).run(parser)` from `mtkclient.Library.mtk_main`. Delegated implementation was not reviewed in depth.
- `_firehose_list.txt`: inventory artifact, not a validated support matrix.

## Checkout and verification

Proposed commands below are documented procedures, not checks executed during this remote review. For a new checkout, use a new/empty destination, not an existing populated project directory:

```powershell
git clone --recurse-submodules https://github.com/krymm/FRP-GONE-NEW.git FRP-GONE-NEW
cd FRP-GONE-NEW
git submodule status --recursive
```

For the existing Windows checkout, inspect and preserve local work first:

```powershell
git -C 'X:\FRP-GONE' status --short
git -C 'X:\FRP-GONE' submodule status --recursive
git -C 'X:\FRP-GONE' submodule foreach --recursive 'git status --short'
```

After fetching and integrating the approved parent change using the local workflow, and resolving any local changes or conflicting submodule remotes:

```powershell
git -C 'X:\FRP-GONE' submodule sync --recursive
git -C 'X:\FRP-GONE' submodule update --init --recursive
git -C 'X:\FRP-GONE' submodule status --recursive
```

Do not add `--force`, reset repositories, or delete existing nested clones to make initialization pass. Sync updates local URL configuration; inspect custom remotes before running it. Completion means all recorded gitlinks resolve, all initialized submodules match the parent-recorded revisions, and nested dependencies initialize successfully. In status output, a leading minus denotes uninitialized, plus denotes a different checked-out revision, and U denotes a conflict.

## Verification and pitfalls

Remote inspection established repository structure, gitlink identities, the existing handoff, selected upstream entry points/manifests, collection commit availability, and EDL's nested Loaders mapping/pin. No clone, submodule initialization, dependency installation, CLI execution, tests, driver installation, or device operations were performed. The mapping repair is not proof of successful fresh checkout or runtime readiness.

Historical setup encountered missing docopt, then started dependency installation without a recorded final success result. Local interpreter, package, driver, and process state remain unknown. Do not treat old background-job handles as current jobs.

Do not infer device support from filenames or the folder name firehoses-pixel-oneplus. Prior Pixel mappings, model/chipset pairings, and partition-behavior claims were speculative. Driver utility presence does not establish a verified driver setup. Interpret Git exit status and actual repository state rather than treating stderr progress alone as failure.

Review caches/session artifacts for repository relevance and sensitive content before proposing cleanup; no exposure is asserted and no deletion is authorized here. Preserve third-party licensing/provenance. Inspect any nested local FRP-GONE directory before moving or removing it.

## Continuation plan

1. Verify the two-file repair diff and confirm all four parent gitlinks are unchanged.
2. Test a fresh recursive checkout in a separate directory. Record exact failures without changing pins; inspect additional nested dependencies if initialization fails.
3. Reconcile the local Windows working tree, remotes, environment, and any untracked project scripts with this snapshot. Preserve local work.
4. Establish isolated setup and safe non-device smoke checks; record observed outcomes separately from historical claims.
5. Define the missing menu/configuration/launcher integration and independently test validation, logging, and failure handling. Keep unsupported device mappings excluded from confirmed support.
6. Review repository hygiene separately and refresh this document after meaningful verification milestones.

## Evidence notes

Sources: supplied conv-hist.txt and project-context-handoff SKILL.md; authenticated GitHub reads of the parent snapshot and pinned upstream sources. The earlier history-only context is superseded where remote inspection provides evidence. Review remains remote-only and non-exhaustive; a working toolkit and successful device servicing have not been demonstrated.
