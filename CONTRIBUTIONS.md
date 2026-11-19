# CM5 tablet upstream contributions

These proposals contribute back to **dvab-sarma's Android 17 device and Rockchip kernel repositories**, which are the base of this port. All three CM5 repositories are actual GitHub forks and retain their upstream history and original copyright notices.

The PRs are drafts because the newly separated product and portable source builders still need a fresh complete build and boot test. Each description distinguishes the development installation's hardware checks from tests still pending. A mergeable GitHub status indicates no textual conflicts; it does not replace hardware regression testing.

| Area | Feature | Upstream PR |
| --- | --- | --- |
| Device | Allow product-specific kernel inputs and USB gadget controller | [#2](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/2) |
| Device | Add an independent Orange Pi CM5 tablet Android product | [#3](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/3) |
| Device | Package AP6256 Wi-Fi firmware and CM5 tablet calibration | [#4](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/4) |
| Device | Package the AP6256 Bluetooth UART firmware patch | [#5](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/5) |
| Device | Add an Android-native wiringOP port with CM5 tablet mapping | [#6](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/6) |
| Device | Add JNI and restricted root-service adapters for the stock wiringOP GUI | [#7](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/7) |
| Device | Add portable CM5 kernel, U-Boot and Android source builders | [#8](https://github.com/dvab-sarma/android_device_opi_opi5_pro/pull/8) |
| Kernel | Use DWARF symbol version generation for the Rockchip Android config | [#7](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/7) |
| Kernel | Add an optional root-only wiringOP MMIO configuration fragment | [#8](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/8) |
| Kernel | Add Orange Pi CM5 tablet base device tree and Android defconfig | [#9](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/9) |
| Kernel | Add HDMI display wiring for the CM5 tablet carrier | [#10](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/10) |
| Kernel | Add AP6256 SDIO Wi-Fi wiring for the CM5 tablet | [#11](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/11) |
| Kernel | Add AP6256 UART Bluetooth wiring for the CM5 tablet | [#12](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/12) |
| Kernel | Merge Android 17 ACK 6.18.39 while preserving Rockchip history | [#13](https://github.com/dvab-sarma/android_kernel_rk_opi/pull/13) |

## Selecting changes

The shared device input/USB override proposal can be reviewed independently. The CM5 product is its own configuration; radio packaging, native wiringOP, the optional original-GUI adapter, and source builders are separate proposals layered on that product. Their descriptions link the required base PRs. The optional vendor GUI APK is not redistributed, and its automated extraction/repackaging helper is not yet included.

The kernel ACK upgrade, DWARF symbol-version configuration and optional MMIO debug fragment are independent shared proposals. The small DWARF and debug PR branches start directly from the existing upstream Android 17 kernel, without including the ACK upgrade. The CM5 base board proposal also starts from that original base. HDMI, Wi-Fi and Bluetooth each share the same base-board commit and add their own include; they do not depend on each other's wiring.

Some feature PR diffs include their unmerged prerequisite commits. Once a prerequisite is merged, GitHub can show the remaining feature delta. The individual proposals can also be cherry-picked in dependency order. The complete published kernel branch retains the proper two-parent ACK merge and all selected features.

The CM5 U-Boot patch, board configuration and portable builder are in the device source-builders proposal. The manifest pins the separate AOSP U-Boot source checkout; U-Boot is not embedded in the Linux repository.

## Source publication

- [CM5 device fork](https://github.com/G-Pereira/android_device_orangepi_cm5_tablet)
- [CM5 kernel fork](https://github.com/G-Pereira/android_kernel_orangepi_cm5_tablet)
- [CM5 manifest fork](https://github.com/G-Pereira/android_manifest_orangepi_cm5_tablet)

The manifest pins the complete device/kernel commits and shared platform dependencies. Development sources are provided; a validated release image is not attached.
