# Android 17 for Orange Pi CM5 Tablet

Based on **[dvab-sarma's Android platform manifests](https://github.com/dvab-sarma/android_local_manifest)**, retaining the original Git history and shared userspace repositories. The kernel workspace project selection derives from [his kernel manifest](https://github.com/dvab-sarma/android_kernel_manifest). His platform integration, Rockchip kernel work, and upstream credits remain the foundation of this port; the original documentation is preserved in `README.upstream.md`.

This manifest targets the existing CM5 on the tablet carrier. It replaces the Pro device and prebuilt-kernel projects with a separate CM5 product and a source kernel. It pins the Android 17 CP2A snapshot, shared dvab-sarma repositories, CM5 device/kernel commits, toolchains, and U-Boot source.

## Checkout

Use two sibling directories on an AOSP Linux build host, with the Android `repo` tool installed:

```sh
mkdir android17 cm5-kernel
cd android17
repo init -u https://github.com/G-Pereira/android_manifest_orangepi_cm5_tablet -b android-17.0
repo sync -j$(nproc)
cd ../cm5-kernel
repo init -u https://github.com/G-Pereira/android_manifest_orangepi_cm5_tablet -b android-17.0 -m kernel.xml
repo sync -j$(nproc)
cd ../android17
```

`default.xml` is the complete Android workspace manifest. `kernel.xml` is the separate Linux/U-Boot/toolchain workspace. Do not combine both in one directory: kernel tooling and Android build definitions otherwise overlap. The inherited `manifest_rk_opi.xml` remains available for upstream reference; it is not the CM5 entry point.

## Build

Follow normal AOSP host setup (the upstream documentation records Ubuntu 24.04). Additional tools include `bc`, `libelf-dev`, `libdw-dev`, `gcc-aarch64-linux-gnu`, `swig`, Python setuptools, `dosfstools`, `e2fsprogs`, `fdisk`, `mtools`, and `rsync`. Preserve the upstream Mesa Python dependencies where required.

Obtain these firmware files from your stock Orange Pi BSP `rkbin` directory; they are not included in this source publication:

```sh
export BL31=/absolute/path/to/rk3588_bl31_v1.45.elf
export ROCKCHIP_TPL=/absolute/path/to/rk3588_ddr_lp4_2112MHz_lp5_2400MHz_v1.16.bin
./device/opi/cm5/opi-cm5-tablet/build_android.sh
```

The wrapper builds the source kernel and CM5 U-Boot, selects `aosp_opi_cm5-cp2a-userdebug`, builds Android, and assembles an 8 GiB SD image under `out/target/product/opi-cm5-tablet/`. `JOBS` overrides the default `nproc` parallelism. A larger SD card may have its userdata partition expanded after flashing. The standard AOSP boot animation is used.

The U-Boot checkout remains a separate AOSP project pinned to `adffd291a17b6c017e73fc6075b91044834f4a26`; the CM5 patch/configuration and builder are maintained in the device repository.

## Status

This is a development source publication. The original development installation has booted Android with HDMI, USB-C ADB, Wi-Fi scanning, Bluetooth initialization, and wiringOP input/readall. The factored CM5 DTB compiles. **A clean full build and boot of the newly separated product and portable wrappers is still pending.** No release image is attached or certified by this publication.

LCD/touch, cameras, audio, battery/charging integration, bus loopback, and electrical GPIO output/interrupt tests remain unverified. The product is userdebug with permissive SELinux; wiringOP MMIO remains root-only, through an optional debug kernel profile. Set `CM5_WIRINGOP_DEBUG=0` to omit that profile.

The native wiringOP tool is source-built. The optional original Android 13 launcher APK is not redistributed; the repository contains the new adapter source, with local APK repackaging still required. See the [device documentation](https://github.com/G-Pereira/android_device_orangepi_cm5_tablet/tree/android-17.0/opi-cm5-tablet) for details.

## Source repositories

- [CM5 device configuration](https://github.com/G-Pereira/android_device_orangepi_cm5_tablet), forked from dvab-sarma's Pro device repository; independent CM5 product under `opi-cm5-tablet/`, shared HAL sources retained.
- [CM5 kernel](https://github.com/G-Pereira/android_kernel_orangepi_cm5_tablet), forked from dvab-sarma's Rockchip kernel; ACK 6.18.39 merge, shared fixes, and separate CM5 board features.
- [This manifest](https://github.com/G-Pereira/android_manifest_orangepi_cm5_tablet), forked from dvab-sarma's Android local manifest.

Feature branches preserve reviewable changes for contribution upstream. This project is an independent community port; original authors retain their copyright and license notices.

See [the contribution index](CONTRIBUTIONS.md) for all feature PRs and their dependencies.
