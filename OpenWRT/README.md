# Version for OpenWRT

The benchmark can be easily crosscompiled, you just have to change the compiler to `mips-openwrt-linux-musl-gcc`. But the 5th benchmark, **ASSIGNMENT**, will be stuck in a forever loop. Here is the workaround and patched edition:

## Workaround

Fix to run on a router with OpenWRT ... TBD.

## Compile on OpenWRT with the SDK and toolchain

First download the toolchain from [downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/](https://downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/) (at the very bottom):

``` sh
apt install build-essential libncurses-dev zlib1g-dev gawk git gettext libssl-dev xsltproc rsync wget unzip python3 zstd
wget https://downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64.tar.zst
tar xvf openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64.tar.zst
make defconfig
make toolchain/install
export PATH=~/github/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64/staging_dir/toolchain-mips_24kc_gcc-14.3.0_musl/bin:$PATH
export STAGING_DIR=~/github/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64/staging_dir
```

Then get nbench

``` sh
wget kreier.org/docs/nbench.tar.gz
tar xf nbench.tar.gz
cd nbench-byte-2.2.3
make
```
