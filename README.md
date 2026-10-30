# kernel-patches

Custom Linux kernel patches for the Lilium kernel, maintained locally.

Forked from [sirlucjan/kernel-patches](https://github.com/sirlucjan/kernel-patches)
(archived), which this repo replaces as the patch source for the
[linux-lilium PKGBUILD](https://github.com/JPratama7/arch-builder).

## Layout

Patches live under a per-kernel-version directory matching the upstream layout:

```
7.3/
  arch-patches-sep/            Arch Linux patches
  bore-patches/                BORE scheduler
  lru-marie-patches/           LRU-MARIE
  lru-marie-rc1-patches/       LRU-MARIE 1.0.0-rc1
  lru-cast-patches/            CAST (self-tuning LRFU, Marie successor)
  poc-selector-patches/        POC scheduler selector
  amd-pstate-patches/
  cachyos-fixes-patches-v2-sep/
  bbr3-cachyos-patches/
  cpu-cachyos-patches/
  cpuidle-patches/
  kbuild-cachyos-patches/
  reflex-patches/
  v4l2loopback-patches/
  adios-iosched-default-on-patches/
  block-patches-all/
  hdmi-patches/
  vesa-patches/
  zram-patches/
  zstd-patches/
  snd-codecs-patches/
  amd-iommu-patches/
  clang-patches/
```

The PKGBUILD fetches patches from

```
https://raw.githubusercontent.com/JPratama7/kernel-patches/main/${_major}/
```

## Adding a new kernel version

1. Create `7.4/` mirroring the layout above.
2. Update the PKGBUILD `_major` (and version-specific paths in `source=()`).
3. Verify with the apply order used by the PKGBUILD's `prepare()`:
   RT patch first, then all patches in `source=` order. Run
   `patch -Np1 -F2 --input=<patch>` on a fresh `linux-$ver` tree and
   confirm no hunk fails with "FAILED".

## Notes

- Patch files are byte-identical to the archived upstream originals
  (sha256sums in the PKGBUILD match).
- Local patches no longer used (e.g. xswap experiments) are kept out of
  this repo.