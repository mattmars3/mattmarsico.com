+++
title = "ESP-IDF On Gentoo"
date = 2026-11-08
description = '''How to install ESP-IDF and other ESP32 development tools on Gentoo.'''
draft = false

[taxonomies]
categories = ["developer-resources"]
tags = ["gentoo"]

[extra] 
toc = true
+++
# ESP-IDF Installation on Gentoo
ESP-IDF is only officially supported on Debian & RHEL-based distros, so here is a guide to getting up-and-running with a manual installation on Gentoo.

## Install Dependencies
Usually, EIM would install these dependencies for us on a supported platform, but in this case we must install (and later maintain) all dependencies manually.
```sh
sudo emerge --ask \
  dev-vcs/git \
  dev-lang/python \
  dev-python/pip \
  dev-build/cmake \
  dev-build/ninja \
  dev-util/ccache \
  app-mobilephone/dfu-util \
  dev-libs/libffi \
  dev-libs/openssl \
  dev-libs/libusb \
  dev-build/flex \
  sys-devel/bison \
  dev-util/gperf
```

## Download EIM
Navigate to the [download site for EIM](https://dl.espressif.com/dl/eim/) (ESP-IDF Installation Manager).

Download a **CLI Installer** that works for you, in this case I chose the x64 version *(eim-cli-linux-x64-v0.21.1.zip)* since I don't need any sort of multilib support.

Once you have downloaded it, unzip it to get the statically-linked binary.

```sh
unzip eim-cli-linux-x64-v*.zip
```

This will reveal a file `eim-v0.xx.y` as well as a symlink `eim` that you can use to run the program. 


## Install the DevKit
Now, use the `eim` binary to install the toolkit. We can skip the prerequisites check since we have manually installed all dependencies.
```sh
./eim install --skip-prerequisites-check
```

If anything goes wrong or dependencies are not installed, the tool is pretty verbose so it should explain what else needs to be installed. If successfully proceed to the next part.

During my installation, it failed to copy the OpenOCD rules so I had to do the following.

```sh
sudo install -Dm644 \
  /home/${USER}/.espressif/tools/openocd-esp32/v0.12.0-esp32-20260703/openocd-esp32/share/openocd/contrib/60-openocd.rules \
  /etc/udev/rules.d/60-openocd.rules
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## Source the environment
```sh
# bash / zsh
source "~/.espressif/tools/activate_idf_v6.1.sh"

# fish
source "~/.espressif/tools/activate_idf_v6.1.fish"
```

## Usage
Now, you should be ready to use the devkit. Check out the [guide to your first project](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/linux-macos-start-project.html) on Espressif's website to get started.
