# OpenWrt for S9xxx-Boxs

Support Amlogic-s9xxx chip series such as S905x3, S905x2, S922x. You can download the OpwnWrt for S9xxx-Boxs firmware from [Releases](https://github.com/ophub/op/releases). Such as `openwrt_s9xxx_${date}`. Then write the IMG file to the USB hard disk through software such as [balenaEtcher](https://www.balena.io/etcher/).

This OpenWrt firmware on the `Github Actions` to packaging was using ***`Flippy's`*** [Amlogic S9xxx Kernel for OpenWrt](https://github.com/ophub/amlogic-s9xxx-openwrt), and the [Installation and Update scripts](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/install-program), etc. Special thanks The maker `Flippy`.

Welcome to use `forks` for personalized OpenWrt firmware configuration. If you like it, Please click the `stars`.

## Firmware instructions

- ***`s9xxx-v*-openwrt_*.img`: For all Amlogic-S9xxx series boxes.*** [🔍](https://www.ebay.com/sch/i.html?_nkw=amlogic)
- `x96-v*-openwrt_*.img`: For X96-Max+(S905x3). [🔍](https://www.ebay.com/itm/133605678868)
- `hk1-v*-openwrt_*.img`: For HK1-Box(S905x3). [🔍](https://www.ebay.com/itm/174515007305)
- `h96-v*-openwrt_*.img`: For H96-Max-X3(S905x3). [🔍](https://www.ebay.com/itm/293499265183)
- `belink-v*-openwrt_*.img` For Belink GT-King. [🔍](https://www.ebay.com/itm/303604712848)
- `belinkpro-v*-openwrt_*.img` For Belink GT-King Pro. [🔍](https://www.ebay.com/itm/324411782338)
- `ugoos-v*-openwrt_*.img` For UGOOS AM6 Plus. [🔍](https://www.ebay.com/itm/254590989143)
- `n1-v*-openwrt_*.img`: For Phicomm-N1.
- `octopus-v*-openwrt_*.img` For Octopus-Planet.

The ***`s9xxx-v*-openwrt_*.img is the general OpenWrt firmware of all Amlogic-S9xxx series boxes`*** . You can write this OpenWrt firmware to the `USB hard disk` to start. When writing into EMMC through [s9xxx-install.sh](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/install-program/files/s9xxx-install.sh), `select the name` of the box you own in the menu.

For more OpenWrt firmware .dtb files are in the [dtb-amlogic](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/armbian/dtb-amlogic) directory. You can use the `s9xxx-v*-openwrt_*.img` firmware to install via USB hard disk. When writing into EMMC through [s9xxx-install.sh](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/install-program/files/s9xxx-install.sh), [select 0: Enter the dtb file name of your box](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/armbian/dtb-amlogic), and use the S9xxx-Boxes you own.

## Install to emmc partition or upgrade instructions

Insert the `USB hard disk` with the written `OpenWrt` firmware. Log in to the default IP: 192.168.1.1 → `Login in to openwrt` → `system menu` → `TTYD terminal` → input command: 

```yaml
s9xxx-install.sh
reboot
```

[For more instructions please see: install-program](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/install-program).


## Compilation method

- Select ***`Build OpenWrt for S9xxx`*** on the [Action](https://github.com/ophub/op/actions) page.
- Click the ***`Run workflow`*** button.

## Configuration file function description

| Folder/file name | Features |
| ---- | ---- |
| .config | Firmware related configuration, such as firmware kernel, file type, software package, luci-app, luci-theme, etc. |
| files | Create a files directory under the root directory of the warehouse and put the relevant files in. You can use custom files such as network/dhcp/wireless by default when compiling. |
| feeds.conf.default | Just put the feeds.conf.default file into the root directory of the warehouse, it will overwrite the relevant files in the OpenWrt source directory. |
| diy-part1.sh | Execute before updating and installing feeds, you can write instructions for modifying the source code into the script, such as adding/modifying/deleting feeds.conf.default. |
| diy-part2.sh | After updating and installing feeds, you can write the instructions for modifying the source code into the script, such as modifying the default IP, host name, theme, adding/removing software packages, etc. |

## .github/workflow/*.yml related environment variable description

| Environment variable | Features |
| ---- | ---- |
| REPO_URL | Source code warehouse address |
| REPO_BRANCH | Source branch |
| FEEDS_CONF | Custom feeds.conf.default file name |
| CONFIG_FILE | Custom .config file name |
| DIY_P1_SH | Custom diy-part1.sh file name |
| DIY_P2_SH | Custom diy-part2.sh file name |
| UPLOAD_BIN_DIR | Upload the bin directory (all ipk files and firmware). Default false |
| UPLOAD_FIRMWARE | Upload firmware catalog. Default true |
| UPLOAD_RELEASE | Upload firmware to release. Default true |
| UPLOAD_COWTRANSFER | Upload the firmware to CowTransfer.com. Default false |
| UPLOAD_WERANSFER | Upload the firmware to WeTransfer.com. Default failure |
| RECENT_LASTEST | maximum retention days for release, artifacts and logs in GitHub Release and Actions. |
| TZ | Time zone setting |
| GITHUB_REPOSITORY | Github.com Environment variables. The owner and repository name. For example, ophub/op. |
| secrets.GITHUB_TOKEN | Personal center: Settings → Developer settings → Personal access tokens → Generate new token ( Name: GITHUB_TOKEN, Select: public_repo ). |

## Firmware compilation parameters

| Option | Value |
| ---- | ---- |
| Target System | QEMU ARM Virtual Machine |
| Subtarget | ARMv8 multiplatform |
| Target Profile | Default |
| Target Images | squashfs |
| LuCI -> Applications | in the file: .config |

## Firmware information

| Name | Value |
| ---- | ---- |
| Default IP | 192.168.1.1 |
| Default username | root |
| Default password | password |
| Default WIFI name | OpenWrt |
| Default WIFI password | none |

