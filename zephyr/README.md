Zephyr Project Port
===================

## Overview

This port is for the Zephyr RTOS Project, available [here](https://www.zephyrproject.org/).

It provides the following zephyr code.

- modules/crypto/wolftpm
    - wolftpm library code
- modules/crypto/wolftpm/zephyr/
    - Configuration and CMake files for wolfTPM as a Zephyr module
- modules/crypto/wolftpm/zephyr/samples/*
    - wolfCrypt test application

## How to setup as a Zephyr Module

### Modify your project's west manifest

Add wolftpm as a project to your west.yml:
```
manifest:
  remotes:
    # <your other remotes>
    - name: wolfssl
      url-base: https://github.com/wolftpm

  projects:
    # <your other projects>
    - name: wolftpm
      path: modules/crypto/wolftpm
      revision: master
      remote: wolfsll
```

If you are using the Nordic nRF Connect SDK with Zephyr, the sdk-nrf manifest
file is located at: `vX.X.X/nrf/west.yml`. On OSX the default installation
location for the nRF Connect SDK is at `/opt/nordic/ncs/vX.X.X`.

Update west's modules:

```bash
west update
```

Now west recognizes 'wolftpm' as a module, and will include it's Kconfig and
CMakeFiles.txt in the build system.

If using the Nordic nRF Connect SDK, to get access to a terminal with west
tool access, open "nRF Connect for Desktop", then "Toolchain Manager",
and finally next to the SDK version you are using click the drop down arrow,
then "Open Terminal".
