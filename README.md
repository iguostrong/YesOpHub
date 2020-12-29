![OPhub logo](/logo.svg)

# OpenWrt Firmware

The latest version of the OpenWrt firmware can be downloaded in [Releases](https://github.com/ophub/op/releases). For detailed information about each firmware, please refer to the README.md file of each model. The currently supported router models are: 

- [Linksys_WRT1900ACS](https://github.com/ophub/op/tree/master/router/linksys_wrt1900acs)
- [Linksys_WRT3200ACM](https://github.com/ophub/op/tree/master/router/linksys_wrt3200acm)
- [Linksys_WRT32X](https://github.com/ophub/op/tree/master/router/linksys_wrt32x)
- [NanoPi_R4S](https://github.com/ophub/op/tree/master/router/nanopi_r4s)
- [NanoPi_R2S](https://github.com/ophub/op/tree/master/router/nanopi_r2s)
- [Phicomm_N1](https://github.com/ophub/op/tree/master/router/phicomm_n1)
- [S9xxx_Boxs](https://github.com/ophub/op/tree/master/router/s9xxx)
- [X86_64](https://github.com/ophub/op/tree/master/router/x86_64)

## Compilation method

- Select ***`Build OpenWrt for ${router}`*** on the [Action](https://github.com/ophub/op/actions) page.
- Click the ***`Run workflow`*** button.

## Related script usage instructions

There are currently two DIY scripts in the root directory of the warehouse: `diy-part1.sh`, `diy-part2.sh` and `.config`, which are executed before and after the update and installation of ` ./scripts/feeds update && ./scripts/feeds install `. You can write the instructions for modifying the source code into the script, such as modifying `the default IP , Host name, theme, add/remove software package...`, etc. If the additional software package has the same name as the existing software package in the OpenWrt source code, the software package with the same name in the Open­Wrt source code needs to be deleted, otherwise the packages in Open­Wrt will be compiled first. It will automatically traverse all files in the `package` directory when compiling.


Just put the `feeds.conf.default` file into the root directory of the warehouse, it will overwrite the relevant files in the Open­Wrt source directory. Create a new `files` directory under the root directory of the warehouse, and put the customized related files in the same directory structure as OpenWrt, and the OpenWrt configuration will be overwritten during compilation.


On the [Action](https://github.com/ophub/op/actions) page. Select ***`Build OpenWrt for ${router}`*** in the list on the left, and Click the ***`Run workflow`*** button on the right. Set ***`SSH connection to Actions: true`*** to use tmate to connect to the `GitHub Actions` virtual server environment. You can directly perform the `make menuconfig` operation to generate the compilation configuration, or any customized operation. After triggering the workflow, wait for the `SSH connection to Actions` step to be executed on the `Actions` page, and then the following three lines of messages will be displayed: 1.` To connect to this session copy-n-paste the following into a terminal or browser`, 2.***` ssh Y26QenMRd@nyc1.tmate.io `***, 3.***` https://tmate.io/t/Y26QenMRd `***. Then copy the `SSH connection command` and paste it into `the terminal` for execution, or copy `the link` to open it in `the browser` and use `the web terminal`. enter the command: ***` cd openwrt && make menuconfig `*** for personalized configuration (The web terminal may encounter a black screen, just press ***`Ctrl+C`***). After completion, press the shortcut key ***` Ctrl+D `*** or execute the ***` exit `*** command to exit, and the subsequent compilation work will proceed automatically.

## router/${firmware} Function description of related files in each firmware package

| Folder/file name | Features |
| ---- | ---- |
| .config | Firmware related configuration, such as firmware kernel, file type, software package, luci-app, luci-theme, etc. |
| files | Create a files directory under the root directory of the warehouse and put the relevant files in. You can use custom files such as network/dhcp/wireless by default when compiling. |
| feeds.conf.default | Just put the feeds.conf.default file into the root directory of the warehouse, it will overwrite the relevant files in the OpenWrt source directory. |
| diy-part1.sh | Execute before updating and installing feeds, you can write instructions for modifying the source code into the script, such as adding/modifying/deleting feeds.conf.default. |
| diy-part2.sh | After updating and installing feeds, you can write the instructions for modifying the source code into the script, such as modifying the default IP, host name, theme, adding/removing software packages, etc. |


## .github/workflow/${workflows_file}.yml files related environment variable description

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

## Firmware information

| Name | Value |
| ---- | ---- |
| Default IP | 192.168.1.1 |
| Default username | root |
| Default password | password |
| Default WIFI name | OpenWrt |
| Default WIFI password | none |

## Catalog description

```shell script

 op
 ├── .github
 │   └── workflows                        
 │       ├── build-openwrt-linksys_wrt1900acs.yml      # Build Linksys WRT1900ACS firmware
 │       ├── build-openwrt-linksys_wrt3200acm.yml      # Build Linksys WRT3200ACM firmware
 │       ├── build-openwrt-linksys_wrt32x.yml          # Build Linksys WRT32X firmware
 │       ├── build-openwrt-x86_64.yml                  # Build X86_64 Virtual Machine firmware
 │       ├── build-openwrt-s905x3.yml                  # Build S905x3 firmware
 │       ├── build-openwrt-phicomm_n1.yml              # Build Phicomm-N1 firmware
 │       ├── build-openwrt-nanopi_r4s-1gb.yml          # Build NanoPi-R4S-1GB firmware
 │       ├── build-openwrt-nanopi_r4s-4gb.yml          # Build NanoPi-R4S-4GB firmware
 │       ├── build-openwrt-nanopi_r2s.yml              # Build NanoPi-R2S firmware
 │       └── delete-older-releases-artifacts.yml       # Delete older releases & artifacts
 │
 ├── router                                            # Related router Openwrt firmware codes 
 │   ├── linksys_wrt1900acs                            # Linksys WRT1900ACS related code files
 │   │   ├── .config                                   # config luci-app, luci-theme and other
 │   │   ├── diy-part1.sh                              # DIY script part 1(Before Update feeds)
 │   │   ├── diy-part2.sh                              # DIY script part 2(After Update feeds)
 │   │   └── README.md                                 # Instructions
 │   │
 │   ├── linksys_wrt3200acm                            # Linksys WRT3200ACM related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   ├── linksys_wrt32x                                # Linksys WRT32X related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │ 
 │   ├── nanopi_r4s                                    # NanoPi R4S related code files
 │   │   ├── .config-1gb
 │   │   ├── .config-4gb
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │ 
 │   ├── nanopi_r2s                                    # NanoPi R2S related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   ├── x86_64                                        # x86_64 related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   ├── phicomm_n1                                    # Phicomm-N1 related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   └── s9xxx                                         # S9xxx-Boxs related code files
 │       ├── .config
 │       ├── diy-part1.sh
 │       ├── diy-part2.sh
 │       └── README.md
 │
 ├── LICENSE                                           # LICENSE for OP
 └── README.md                                         # Instructions for OP
   
```

## Acknowledgments

- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Lienol/openwrt](https://github.com/Lienol/openwrt)
- Flippy: The maker of Amlogic s9xxx Kernel for openwrt 
- [P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)
- [tuanqing/mknop](https://github.com/tuanqing/mknop)

- [Mikubill/transfer](https://github.com/Mikubill/transfer)

## License

[LICENSE](https://github.com/ophub/op/blob/main/LICENSE) © OPHUB
