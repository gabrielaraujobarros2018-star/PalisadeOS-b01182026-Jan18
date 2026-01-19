PalisadeOS — Current State README
Build: b01182026
Date: 2026-01-18

============================================================
PROJECT INTENT
============================================================

PalisadeOS is a low-level experimental operating system designed to be
booted on real hardware, targeting both PCs and mobile-class devices
(Android-class) with a single kernel philosophy.

Current focus:
- Firmware → bootloader → kernel correctness
- Real boot paths only
- No GUI, no polish, no abstractions unless demanded by hardware

This build explicitly prioritizes "boots on hardware" over features.

============================================================
KERNEL STATUS
============================================================

Kernel state as of b01182026:

- Kernel exists as a standalone ELF
- Entry point and linker script are under active validation
- No dependency on userspace, init, or services
- No GUI, no framebuffer requirements
- No SMP, no drivers beyond what is strictly required to boot

Kernel goals at this stage:
- Be loadable by a standards-compliant bootloader
- Reach kernel entry reliably
- Execute early init code without faulting
- Provide basic logging/inspection capability

Kernel work is intentionally frozen unless:
- A bootloader demands changes
- Hardware execution reveals a fault

============================================================
BOOTLOADER: LIMINE
============================================================

Chosen bootloader:
- Limine (v10.x)

Reason for selection:
- Multiboot-style simplicity
- Supports BIOS and UEFI
- Suitable for early-stage kernel bring-up
- Minimal policy imposed on kernel

Current Limine state:

- Clean Limine v10.x source tree present
- Source obtained as a release archive (not a git submodule)
- No build artifacts generated yet

Missing artifacts:
- limine-bios.sys
- limine-bios-cd.bin
- limine-install
- UEFI binaries (deferred)

============================================================
WHY LIMINE IS NOT BUILT YET
============================================================

Build is blocked due to environment limitations:

- Development is being done inside Termux (Android)
- Autotools toolchain is incomplete
- `aclocal` (automake) is missing
- `autoreconf -fi` fails immediately

Because of this:
- Limine cannot be configured
- Limine cannot be built
- No BIOS or UEFI binaries exist yet

This is an environment issue, not a Limine or kernel issue.

============================================================
ISO / BOOT MEDIA STATUS
============================================================

- ISO directory structure exists
- `/iso/boot` exists
- No valid boot sector or Limine stage1 present
- xorriso invocation fails correctly due to missing Limine binaries

No fake or placeholder boot images were generated.

============================================================
WHAT WAS *NOT* DONE (INTENTIONALLY)
============================================================

- No refactors
- No fake binaries
- No hand-written boot sectors
- No copying prebuilt Limine binaries from unknown sources
- No kernel changes to “make things work”
- No scope expansion

All failures observed are real and expected given the environment.

============================================================
NEXT STEPS (FROZEN PLAN)
============================================================

Immediate next step (outside this session):
- Restore a proper build environment for Limine
  - Either full Termux autotools stack
  - Or external PC build host

Once Limine builds:
1. Generate BIOS artifacts
2. Place Limine files under `/boot/limine/`
3. Write minimal `limine.cfg`
4. Build ISO correctly
5. Attempt first real boot on PC hardware

Kernel changes will only be made if Limine explicitly requires them.

============================================================
SUMMARY
============================================================

This build ends in a clean, honest state:

- Kernel exists and is intentionally minimal
- Bootloader choice is finalized
- Environment limitations are identified
- No technical debt or fake progress introduced

b01182026 is a valid checkpoint, not a failure.
