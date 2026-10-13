# Historical RP2350 build record

This record describes the preserved build made on 14 August 2026. Publishing it on 13 October 2026 did not rebuild or modify the firmware.

- Merge commit: `980930007b91f65cb36c10d5a30a6fef8cf7cfcc`
- Official beta1 parent: `8bdb00cf5c5308419c35dfcc36f72b7d01bbc4bd`
- Overhaul parent: `7c3c7bf034e73425538e0169d352993536f3dbdb`
- Pico SDK 2.2.0: `a1438dff1d38bd9c65dbd693f0e5db4b9ae91779`
- GNU Arm Embedded Toolchain 10-2020-q4-major, GCC 10.2.1
- Target: Pico 2, RP2350 Arm Secure, Release; `DSPI_LOOPBACK=OFF`
- Clock diagnostics enabled: `DSPI_CLOCK_DIAG=1`
- Firmware version 1.1.6; bulk format V28; preset slot V35; preset directory V18

## Preserved artifacts

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `DSPi-RP2350-v1.1.6-beta1-SPDIF-RX-Overhaul-Test.uf2` | 491,520 | `977B5DC610E647386F350B7A45A37D5E3613923AF38296E8E563EE800B1CEEB9` |
| `DSPi-RP2350-v1.1.6-beta1-SPDIF-RX-Overhaul-Test.bin` | 245,320 | `07E33051A39E8106625DA8FE2B13289827CF8EA92B30DFAB8F3EBF6B6005B6CD` |

## Recorded August validation

- Full RP2350 compile/link: passed, 140 build steps.
- Linker RAM-pull safety assertion: passed.
- RAM placement Check A, hot code closure Check B and Core-1 literal Check B2: zero failures; cold-path veneer warnings retained.
- `.data`: 85,080 bytes; `.bss`: 362,344 bytes; free RAM: 74,544 bytes.
- **Existing `.data` regression ceiling: failed by 9,304 bytes**, against the 75,776-byte limit. The limit was not raised or bypassed.
- Crossover numerical suite: 288/288 configurations passed.
- Non-hardware harness: passed through group 32. The final worker-pipe test could not run on Windows because its POSIX `select()` implementation raised `WinError 10038`.
- Git whitespace check: passed.

These results are not a full test pass or proof of dropout-free hardware operation. At publication, the saved artifact hashes and unchanged firmware source were checked; the historical numerical/build results above were not rerun.
