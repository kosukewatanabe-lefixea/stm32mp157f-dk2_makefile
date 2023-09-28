# STM32MP1_FOR_M4

## environments

```sh
kwatanabe@laptop01:~/Lapps/STM32MP1_for_M4/method_1$ make --version

GNU Make 4.3
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

## Method1 :

- Makefile:
  - Copy from Distribution-Package/layers/meta-st/meta-st-stm32mp/recipes-extended/m4projects/files/Makefile.stm32
  - comment out

```makefile
# before
include $(BUILD_OUT)/conf/config.in
# after
# include $(BUILD_OUT)/conf/config.in
```

- stm32mp15xx_m4.ld

  - Copy from Distribution-Package/build-openstlinuxweston-stm32mp1/workspace/sources/m4projects-stm32mp1/Drivers/CMSIS/Device/ST/STM32MP1xx/Source/Templates/gcc/linker/stm32mp15xx_m4.ld

- nosys.specs

  - Copy from Distribution-Package/build-openstlinuxweston-stm32mp1/tmp-glibc/sysroots-components/x86_64/gcc-arm-none-eabi-native/usr/share/gcc-arm-none-eabi/arm-none-eabi/lib/nosys.specs

- nano.specs :

  - Copy from Distribution-Package/build-openstlinuxweston-stm32mp1/tmp-glibc/sysroots-components/x86_64/gcc-arm-none-eabi-native/usr/share/gcc-arm-none-eabi/arm-none-eabi/lib/nano.specs

  ```sh
  kwatanabe@laptop01:~/Lapps/STM32MP1_for_M4/method_1$ make all
  link out/m4.elf
  arm-ostl-linux-gnueabi-gcc  -Wl,-O1 -Wl,--hash-style=gnu -Wl,--as-needed   -specs=nosys.specs -specs=nano.specs -Wl,-Map=./out/output.map -Wl,--gc-sections -lm -o out/m4.elf.sym   -T stm32mp15xx_m4.ld
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find crt1.o: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find crti.o: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find crtbegin.o: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lm: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc_s: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lc_nano: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc_s: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lgcc_s: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lc_nano: No such file or directory
  /home/kwatanabe/st/Developer-Package/SDK/sysroots/x86_64-ostl_sdk-linux/usr/libexec/arm-ostl-linux-gnueabi/gcc/arm-ostl-linux-gnueabi/12.2.0/ld: cannot find -lnosys: No such file or directory
  collect2: error: ld returned 1 exit status
  make: *** [Makefile:76: out/m4.elf] Error 1
  ```
