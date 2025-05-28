# MPU Underflow Attack Example

This example demonstrates an underflow attack on ARM Cortex-M boards that can cause a kernel crash.

## Description

The application attempts to trigger an underflow in the MPU region calculation by calling `memop(0, 536907776)` where:
- `memop(0, ...)` is the `brk` system call
- `536907776` (0x20018000) is a hardcoded memory start address

This causes `num_enabled_subregions0 - 1` to underflow when `new_app_break == region_start` in the kernel's `update_app_memory_region` function.

## Impact

This vulnerability can crash the kernel, resulting in a denial of service attack.

## Note

This is a proof-of-concept demonstration. The hardcoded memory address may need to be adjusted for different boards or memory layouts.