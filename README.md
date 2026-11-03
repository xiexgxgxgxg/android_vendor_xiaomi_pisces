# android_vendor_xiaomi_pisces

Xiaomi Mi 3 TD（pisces）的专有 blob，提取自 MIUI **V9.2.3.0.KXCCNEK**（Android 4.4）
官方线刷包 `pisces_images_V9.2.3.0.KXCCNEK_20171229.0000.00_4.4_cn`。

## 分支

| 分支 | 用途 |
|---|---|
| `lineage-16.0` | **当前**：LineageOS 16.0（Android 9）使用 |
| `cm-11.0` | 旧 CM11 存档 |

## 内容

- **186 个文件，约 60 MB**
- Tegra HAL：`gralloc.tegra` / `hwcomposer.tegra` / `audio.primary.tegra` /
  `audio_policy.tegra` / `camera.tegra` / `gps.tegra` / `sensors.pisces` /
  `lights.pisces` / `nfc.tegra`
- NV 图形：`libnvrm`、`libnvrm_graphics`、`libEGL_tegra`、`libGLESv*_tegra`
- 媒体：`libnvomx`、`libnvomxilclient`、`libnvomxadaptor`
- 无线/蓝牙：BCM43341 固件（`vendor/firmware/bcm43341/*`）
- keylayout / idc / 权限 XML

## 来源与再生成

提取流程（目标机）：

```bash
# 1) 解包线刷包，取出 system.img
tar -xzf pisces_images_*.tgz
# 2) sparse -> raw（可用 AOSP 的 simg2img，或任意 Android sparse 解析器）
# 3) 提取文件系统（无需 root）
debugfs -R "rdump / /path/to/system" system.raw.img
# 4) 按 device/xiaomi/pisces 的 proprietary 清单拷贝到 proprietary/ 并生成 pisces-vendor.mk
```

`pisces-vendor.mk` 由脚本生成，使用 `PRODUCT_COPY_FILES` 把
`proprietary/<path>` 安装到 `system/<path>`。

## 说明

- `libImmVibeJ.so` 不在此仓库（由 `hardware/nvidia/pisces/immersion` 提供）
- 缺失 2 个 NFC `*.ncd` 配置文件（MIUI 包中不存在，不影响启动）
