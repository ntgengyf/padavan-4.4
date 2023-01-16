# padavan-4.4 #

这个项目是基于原始的 rt-n56u 和最新的 mtk 4.4.198 内核，这是从 D-LINK GPL 代码中获取的。

- 特征
  - 基于 4.4.198 Linux 内核
  - 支持基于MT7621的设备
  - 支持MT7615D/MT7615N/MT7915D无线芯片
  - 支持 raeth 和 mt7621 hwnat with legency 驱动
  - 支持 qca shortcut-fe 功能
  - 支持基于netfilter的IPv6 NAT
  - 支持集成在内核中的 WireGuard
  - 支持 fullcone NAT (by Chion82)
  - 支持通过sysfs控制LED&GPIO


- 支持的设备
  - CR660x
  - JCG-Q20
  - JCG-AC860M
  - JCG-836PRO
  - JCG-Y2
  - DIR-878
  - DIR-882
  - K2P
  - K2P-USB
  - NETGEAR-BZV
  - MR2600
  - MI-4
  - MI-R3G
  - MI-R3P
  - R2100
  - XY-C1

- 编译步骤
  - 安装依赖
    ```sh
    # Debian/Ubuntu
    sudo apt install unzip libtool-bin curl cmake gperf gawk flex bison nano xxd \
        fakeroot kmod cpio git python3-docutils gettext automake autopoint \
        texinfo build-essential help2man pkg-config zlib1g-dev libgmp3-dev \
        libmpc-dev libmpfr-dev libncurses5-dev libltdl-dev wget libc-dev-bin

    # Archlinux/Manjaro
    sudo pacman -Syu --needed git base-devel cmake gperf ncurses libmpc \
            gmp python-docutils vim rpcsvc-proto fakeroot cpio help2man

    # Alpine
    sudo apk add make gcc g++ cpio curl wget nano xxd kmod \
        pkgconfig rpcgen fakeroot ncurses bash patch \
        bsd-compat-headers python2 python3 zlib-dev \
        automake gettext gettext-dev autoconf bison \
        flex coreutils cmake git libtool gawk sudo
    ```
  - 克隆源代码
    ```sh
    git clone --depth=1 https://github.com/vb1980/Padavan-KVR.git /opt/rt-n56u
    ```
  - 准备工具链
    ```sh
    cd /opt/rt-n56u/toolchain-mipsel

    # （推荐）为 x86_64 或 aarch64 主机下载预构建的工具链
    ./dl_toolchain.sh

    # 或者使用 crosstool-ng 构建工具链
    # ./build_toolchain
    ```
  - 修改模板文件并开始编译
    ```sh
    cd /opt/rt-n56u/trunk

    # （可选）修改模板文件
    # nano configs/templates/K2P.config

    # 开始编译
    fakeroot ./build_firmware_modify K2P

    # 要为其他设备构建固件，请在上一次构建后清理树
    ./clear_tree
    ```

- 说明
  - 通过 sysfs 控制 GPIO 和 LED
  - NAND RWFS分区使用方法
  - How to use IPv6 NAT and fullcone NAT
  - How to add new device support with device tree
