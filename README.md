<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">QEMU iPod Guide</h3>

  <p align="center">
    This is a simple and quick guide on how to set up devos50's QEMU iPod Emulator.
    <br />
    For Apple Silicon Macs!
    <br />
    <a href="https://github.com/devos50/qemu"><strong>View Repository »</strong></a>
    <br />
    <br />
    <a href="https://github.com/devos50">View Author</a>
    ·
    <a href="https://devos50.github.io/blog/2022/ipod-touch-qemu-pt2">View Instructions</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/blob/master/README.md">Credits</a>
    <br />
    <br />
  </p>
</div>

## About This Guide

<p align="center">
  <img src="images/iPod.png" alt="iPod">
</p>

There is a lot of confusion with the original instruction guide linked above, so this guide will solve all the confusion :smile:

<b>Here's why:</b>
* Short and easy to follow steps
* Saves time and reduces errors
* Simple copy and pasting

### Built With

This section should list any major frameworks/libraries used to bootstrap your project. Leave any add-ons/plugins for the acknowledgements section. Here are a few examples.

* [![Next][Next.js]][Next-url]
* [![React][React.js]][React-url]
* [![Vue][Vue.js]][Vue-url]
* [![Angular][Angular.io]][Angular-url]
* [![Svelte][Svelte.dev]][Svelte-url]
* [![Laravel][Laravel.com]][Laravel-url]
* [![Bootstrap][Bootstrap.com]][Bootstrap-url]
* [![JQuery][JQuery.com]][JQuery-url]

## Getting Started

This project requires Homebrew

Follow the install instructions before continuing

### Install QEMU & Friends

```sh
brew install qemu && brew install ninja && brew install make &&
brew install pkg-config && brew install meson && brew install sdl2
```

### Build QEMU

```sh
mkdir iPod && cd iPod && git clone https://github.com/devos50/qemu && cd qemu && git checkout ipod_touch_1g
&& mkdir build && cd build && ../configure --enable-sdl --disable-cocoa --target-list=arm-softmmu --disable-capstone
--disable-pie --disable-slirp --extra-cflags=-I/opt/homebrew/opt/openssl@3/include --extra-ldflags='-L/opt/homebrew/opt/openssl@3/lib -lcrypto' && make -j8
```

### Download iPod Files

```sh
cd ../.. && mkdir boot && cd boot
&& curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/bootrom_s5l8900
&& curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/iboot_204_n45ap.bin
&& curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/nand_n45ap.zip
&& curl -LJO https://github.com/devos50/qemu-ios/releases/download/n45ap_v1/nor_n45ap.bin
&& unzip nand_n45ap.zip && rm nand_n45ap.zip && rm -rf __MACOSX
```
### Run QEMU

```sh
cd .. && echo "cd qemu/build && ./arm-softmmu/qemu-system-arm -M iPod Touch,bootrom=../../boot/bootrom_s5l8900,
iboot=../../boot/iboot_204_n45ap.bin,nand=../../boot/nand -serial mon:stdio -cpu max -m 1G -d unimp -pflash ../../boot/nor_n45ap.bin" > run.sh && sh run.sh
```

### FINAL NOTES

To run the iPod simple type in the terminal from the ./iPod folder

```sh
sh run.sh
```
