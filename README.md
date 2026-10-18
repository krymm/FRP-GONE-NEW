# FRP-GONE

A Windows-oriented phone-servicing toolkit that bundles well-known open-source flashing and exploit tooling as Git submodules, with a planned launcher/menu layer on top.

> **Project status:** early-stage scaffold. This repository currently contains only submodule references and planning notes. The menu/launcher integration described in `PROJECT_CONTEXT.md` is **planned but not yet implemented**, and nothing here has been verified end-to-end against real hardware.

## What this repository is

FRP-GONE aggregates proven upstream tools for Qualcomm (EDL/Firehose) and MediaTek (MTK) device servicing via Git submodules. The long-term goal is a single Windows entry point (`menu.bat`) that launches the appropriate tool per SoC family, with bundled drivers and programmer/loader collections.

**Intended use:** servicing phones you own or are explicitly authorized to service.

## Repository layout

| Path | Type | Description |
|---|---|---|
| `edl/` | submodule | [bkerler/edl](https://github.com/bkerler/edl) — Qualcomm EDL / Firehose client (`edl.py`, `edlclient/`, `src/`, `Makefile`) |
| `mtk/` | submodule | [bkerler/mtkclient](https://github.com/bkerler/mtkclient) — MediaTek client & DA loader/exploit tooling (`mtk.py`, `mtkclient/`, `custom/`, `setup/`) |
| `Firehose/` | submodule | [SMAAN9810/Firehose-Programmer-Collection](https://github.com/SMAAN9810/Firehose-Programmer-Collection) — Qualcomm firehose programmer collection |
| `firehose-mcp/` | submodule | [feravoltza/firehose-mcp](https://github.com/feravoltza/firehose-mcp) — firehose programmer collection (includes `MBR.mbr` + GPT backups) |
| `_firehose_list.txt` | file | Inventory of ~500 `.mbn` programmer filenames (filenames only — no contents, metadata, or device mapping) |
| `PROJECT_CONTEXT.md` | file | Handoff/status document describing what exists vs. what is planned |
| `.gitmodules` | file | Submodule definitions (URLs and paths) |

## Prerequisites

- **Git** with submodule support.
- **Python 3** — required by both `edl` and `mtkclient`. Consult each submodule's own requirements for exact versions and dependencies.
- **Windows-specific driver setup** — EDL and MTK flashing require proper USB/portal drivers on the host. Driver installation steps referenced in `PROJECT_CONTEXT.md` have **not been verified**.
- Note: `mtkclient` historically depends on Linux-style USB access; check its upstream docs before assuming full Windows support.

## Getting started

Because everything lives in submodules, clone recursively:

```bash
git clone --recursive https://github.com/<your-fork>/FRP-GONE.git
cd FRP-GONE
```

If you already cloned without `--recursive`, initialize the submodules:

```bash
git submodule update --init --recursive
```

This also fetches nested submodule content (e.g., `mtk/Loaders`, which points at `bkerler/mtk-bypass-loaders`).

To pull submodule updates later:

```bash
git submodule update --remote --merge
```

Check pin state at any time with:

```bash
git submodule status
```

Lines prefixed with `-` mean the submodule is not initialized locally; `+` means the checked-out commit differs from the pinned one.

## Usage notes

Each submodule keeps its own CLI and documentation — this repo does not yet wrap them:

- **Qualcomm (EDL):** run from inside `edl/`, e.g. `python edl.py ...`. See `edl/README.md` (upstream).
- **MediaTek (MTK):** run from inside `mtk/`, e.g. `python mtk.py ...`. See `mtk/README.md` and `mtk/setup/` (upstream).
- **Programmer/loader collections:** `Firehose/` and `firehose-mcp/` hold programmer images used *by* the EDL tool. Treat `_firehose_list.txt` as an unverified inventory list only — do not infer device support from filenames.

## Scope, safety, and legality

- These tools can permanently modify or brick devices. Use on test hardware first; back up before writing.
- Bypassing factory reset protection on devices you do not own or are not authorized to service may be illegal in your jurisdiction. Authorized device servicing and research only.
- Nothing in this repository has been validated against real devices; treat all workflow claims as unverified until tested.

## Roadmap (from PROJECT_CONTEXT.md)

Planned, not implemented:

1. Top-level `menu.bat` launcher routing to the correct tool per SoC family.
2. Bundled driver installer steps for Windows.
3. Verified programmer→device mapping (the current `_firehose_list.txt` is filenames only).

## Disclaimer

This project wraps third-party open-source tools maintained by their respective authors (`bkerler`, `SMAAN9810`, `feravoltza`). Upstream licenses and terms apply to each submodule. Use entirely at your own risk.
