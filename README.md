# QEMU-iPod-Guide
This is a simple &amp; quick guide on how to set up [link](devos50)'s [link](QEMU iPod Emulator). For Apple Silicon Macs.

https://devos50.github.io/blog/2022/ipod-touch-qemu-pt2/


## Getting Started!

blah blah blah

### Prerequisites

blah blah blah

# Install Homebrew

[link]


# Install QEMU & Friends

```sh
brew install qemu && brew install ninja && brew install make && brew install pkg-config && brew install meson && brew install sdl2
```



# Build QEMU

```sh
mkdir iPod && cd iPod && git clone https://github.com/devos50/qemu && cd qemu && git checkout ipod_touch_1g
```

```sh
mkdir build && cd build && ../configure --enable-sdl --disable-cocoa --target-list=arm-softmmu --disable-capstone --disable-pie --disable-slirp --extra-cflags=-I/opt/homebrew/opt/openssl@3/include --extra-ldflags='-L/opt/homebrew/opt/openssl@3/lib -lcrypto' && make -j8
```

# Download iPod Files

```sh
cd ../.. && mkdir boot && cd boot && curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/bootrom_s5l8900 && curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/iboot_204_n45ap.bin && curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/nand_n45ap.zip && curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/nor_n45ap.bin
```

```sh
unzip nand_n45ap.zip && rm nand_n45ap.zip && rm -rf __MACOSX
```
# Run QEMU

```sh
cd .. && echo "cd qemu/build && ./arm-softmmu/qemu-system-arm -M iPod-Touch,bootrom=../../boot/bootrom_s5l8900,iboot=../../boot/iboot_204_n45ap.bin,nand=../../boot/nand -serial mon:stdio -cpu max -m 1G -d unimp -pflash ../../boot/nor_n45ap.bin" > run.sh && sh run.sh
```

# FINAL NOTES

To run the iPod simple type in the terminal from the ./iPod folder

```sh
sh run.sh
```
