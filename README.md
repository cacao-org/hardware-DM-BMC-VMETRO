# hardware-DM-BMC-VMETRO
VMETRO interface to BMC DM


Original driver is for kernel 2.6

## Changes required for kernel 5.4

Kernel space code (kernel module):
- change "asm/uacess.h" to "linux/uaccess.h" in dpio2-linux-kernel-module.c include statement
- change "ioctl" to "unlocked_ioctl", and remove inode entry in dpio2_ioctl (see 
https://stackoverflow.com/questions/23708661/how-to-call-compat-ioctl-or-unlocked-ioctl/23710544)
- change "page_cache_release()" to "put_page()"
- Add "EXTRA_CFLAGS += -Wno-error=date-time" to Makefile
- Add "cp $(MODULE_NAME).ko ../../../../rh-test-src/" to Makefile

User space :
- add "-std=g++11" to compile flag to remove "gets" error

Application (in rh-test-src directory) :
- change PRJ_HOME to: "PRJ_HOME = $(PWD)/.." in Makefile
- add "-fPIE" to CC_OPTIM in Makefile
- add "$(DRIVER)" to rm list in clean target


