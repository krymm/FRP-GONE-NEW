# FRP GONE — Project Context and Handoff

Updated: October 15, 2026, 10:54 AM CST (Regina, Saskatchewan)
Project root: `X:\FRP-GONE\`
Status: Provisional, history-grounded handoff; current local implementation not inspected.
Snapshot: Branches, commits, working-tree changes, and repository instructions unknown.
Audience: A coding agent with access to the Windows project directory but no prior conversation.

## Goal and constraints

Build a Windows phone-servicing toolkit with an interactive menu, model-specific batch launchers, supporting runtimes/tools, programmer files, setup documentation, and a reusable project skill. The original user request focused on FRP-related servicing using Qualcomm Firehose tooling. MediaTek support was also discussed, but no completed integration is evidenced.

User requirements and constraints:
- Use `X:\FRP-GONE\` as the project root.
- Include required supporting files in the project structure rather than supplying only instructions.
- Use GitHub and web search for research and sourcing; do not use Firecrawl or Hugging Face.
- Preserve a structure that allows additional models to be added later.

This document records project intent, not validated authorization, device compatibility, or readiness for device operations. Establish the scope of authorized servicing before implementing device-changing functionality.

## Evidence and review limits

Sources: supplied `conv-hist.txt`, supplied `SKILL.md` (project-context-handoff), and the user's explicit project-root designation.

The conversation contains planning, speculative technical claims, and selected historical Windows command output. Treat these separately: command output supports only what was observed at that time; an earlier assistant statement does not establish implementation or successful operation.

No current local files, Git metadata, existing handoff documents, or repository instructions were inspected while drafting this document. No environment changes, downloads, dependency installations, or phone operations were performed. No existing local document was overwritten. Reconcile this draft with the accessible codebase before presenting it as a current implementation snapshot.

## Current implementation

Historical command output supports the following limited observations:

| Relative path | Reported source and contents | Status |
|---|---|---|
| `edl\` | `bkerler/edl`; `edl.py` existence check returned true; root listing included `edlclient\`, `edl.bat`, `Drivers\`, and `Loaders\` | Historically observed; current state and runtime unverified |
| `firehoses\` | `zenlty/Qualcomm-Firehose`; a top-level listing reported 163 entries | Historically observed; exact usable-file count and device compatibility unverified |
| `firehoses-pixel-oneplus\` | `thantoeaungat/firehose`; listings included assorted OnePlus, Samsung, and generic programmer filenames | Historically observed; folder name does not prove Pixel support |
| `mtk\` | `bkerler/mtkclient`; root listing included `mtk.py`, `mtk.bat`, `mtkclient\`, and `Setup\` | Historically observed; runtime unverified |

The following deliverables were planned, but their creation was not demonstrated:
- Main interactive menu, proposed as `FRP-GONE.bat` or `frp_gone.bat`.
- Shared launcher and model-specific wrappers under a proposed `models\` directory.
- Setup script, proposed as `install-tools.bat` or another dependency-installer name.
- Project `README.md`, consolidated driver organization, and `_logs\`.
- A reusable FRP GONE local skill.

Do not assume these files are absent today; inspect the working tree. The attached `SKILL.md` describes the handoff workflow, not proof that the separate FRP GONE project skill was created.

## Code map and intended flow

Historically observed navigation points:
- `edl\edl.py` / `edl\edlclient\`: Qualcomm tooling entry point and implementation.
- `edl\requirements.txt`: dependency manifest used by the attempted installation.
- `edl\Drivers\Windows\`: listing included `Install_Windows.bat`, `zadig-2.8.exe`, and `libusb-1.0.26-binaries.7z`.
- `mtk\mtk.py` / `mtk\mtk.bat`: MediaTek entry points. An earlier attempt used an incorrect entry-point path before the root listing clarified it.
- `mtk\requirements.txt`: dependency manifest targeted by the installation attempt.
- `mtk\Setup\`: inspected listing showed Linux setup resources; a bundled Windows driver package was not established there.

Intended architecture, not implemented evidence: menu selection → model-specific configuration/wrapper → shared tool launcher → underlying tool, with setup and logging handled consistently. The exact configuration format and naming convention remain undecided.

There is no verified project-level setup, run, or test command. Inspect scripts before executing them; do not derive executable device-changing procedures from the speculative historical notes.

## Decisions, mismatches, and pitfalls

- Programmer compatibility remains unresolved. The prior discussion guessed that names such as `3_emmc_ddr.mbn` identified Pixel devices. No confirming mapping was established. Keep these unsupported rather than adding them as working menu options.
- Earlier statements about partition formatting, FRP behavior, chipset/model pairings, and tool arguments were speculative. Validate against the actual tool version and device-specific evidence before using them as requirements.
- Listed Zadig/libusb utilities do not substantiate the earlier claim that a particular signed Qualcomm driver package had been downloaded and verified. Driver availability and suitability remain unresolved.
- Git progress written to stderr was interpreted as failure by a prior PowerShell invocation. Later path/listing checks showed repository contents. Inspect actual process status and repository integrity rather than treating stderr alone as failure or assuming every nonzero exit was harmless.
- A nested `X:\FRP-GONE\FRP-GONE\` directory was described as empty. Its purpose is unknown. Do not delete or relocate it without inspection.
- Earlier suggestions to install packages globally were not a settled environment strategy. Inspect existing environments before proposing changes; do not install dependencies just to prepare a handoff.

## Verification and precise resume point

Historical checks: selected directory listings, entry-point existence checks, driver-resource listings, and dependency-manifest reads. An attempted help invocation encountered a missing `docopt` dependency.

A background installation was then started for the EDL and MediaTek requirement sets. The supplied record contains no final success result. Do not assume dependencies were installed or that a process is still running; historical background-job handles cannot establish current process state.

The last evidenced work involved dependency installation, MediaTek setup resources, and uncertain programmer-to-device mappings. No finished menu, confirmed phone-support matrix, successful hardware connection, end-to-end servicing result, or automated test pass was established.

## Continuation plan

Proposed sequence, subject to the current repository instructions:

1. Inspect the root read-only. Locate applicable instructions, existing context/state files, top-level scripts, manifests, and repository boundaries. Capture branch, commit, and working-tree status for each relevant repository. Completion: an evidence-backed inventory without modifying files.
2. Reconcile planned deliverables with actual files. Trace any menu through its model configuration and launcher. Completion: each material component classified as verified, implemented but unverified, partial, planned, or unknown.
3. Establish environment state. Inspect interpreter selection, virtual environments, manifests, installation logs, and script contents. Use safe, targeted checks only where appropriate. Completion: documented prerequisites and exact observed blockers, without speculative installation-success claims.
4. Establish supported-device evidence. Record exact model/variant, tool version, programmer provenance, and the basis of each compatibility claim. Completion: unsupported mappings remain explicitly excluded from confirmed support.
5. Propose the smallest remaining implementation work in dependency order. Separate read-only diagnostics from device-changing functions and obtain required approval before side effects. Completion: a scoped plan tied to actual paths, not the old speculative backlog.
6. Refresh the dedicated handoff using inspected evidence. Reuse an existing unambiguous handoff file; otherwise use `PROJECT_CONTEXT.md` at the project root. Preserve unrelated content and obey write-confirmation requirements. Completion: saved document checked against its intended content and diff where available.

## Readiness summary

The historical evidence establishes downloaded source trees and preliminary investigation, not a ready-to-run toolkit. The immediate next step is local read-only reconciliation, not another download, dependency installation, or device operation.
