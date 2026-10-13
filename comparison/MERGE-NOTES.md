# What the historical merge contains

This repository shares the experimental RP2350 source and image tested on my ESP32 S/PDIF music-player rig. It is not a proposed minimal cherry-pick or a merge into current upstream main.

## Source provenance

`980930007b91f65cb36c10d5a30a6fef8cf7cfcc` is a two-parent merge of official v1.1.6-beta1 (`8bdb00cf5c5308419c35dfcc36f72b7d01bbc4bd`) and the complete S/PDIF RX overhaul tip (`7c3c7bf034e73425538e0169d352993536f3dbdb`). It does not contain the later beta2/beta3/beta4 effects or the October upstream integration changes.

The diff from beta1 spans 39 files. It brings over the receiver/rate-estimation work, shared input servo and soft VCXO, free-running S/PDIF and I2S output DMA rings, associated USB-feedback and pipeline changes, clock diagnostics and architecture notes. These are coupled changes: the hardware observations do not establish which individual component affected the audible result.

## Compatibility resolutions

- Retain beta1's input-capture arena ownership and claim/release changes alongside the overhaul receiver and servo.
- Keep beta1's ADAT output starvation-rebaseline API still called by `main.c`, alongside the ring-output implementation.
- Remove the obsolete RAM-validator requirement for output DMA IRQ handlers: the overhaul replaces those handlers with free-running rings.
- Allow both Linux `.o` and Windows `.obj` object names in the RP2350 memory-map patterns without disabling the RAM-placement assertion.
- Preserve beta1 control-surface and firmware-format compatibility.

## Exact image, not the working directory

The release includes the original 491,520-byte UF2, its 245,320-byte BIN and hashes. See [the build record](BUILD-RECORD.md) for toolchain, SDK, validation results and the failed memory-regression check.

The later uncommitted change to `tools/clkdiag_poll.py` is excluded because it is not part of the original source commit or UF2. Logs and scratch build directories are also excluded. The original merge is available directly from the release tag; the only publication additions on main are documentation.

This build was useful on my particular rig. That is hardware feedback, not evidence that the entire merge is upstream-release-ready or that one specific change fixes every dropout.
