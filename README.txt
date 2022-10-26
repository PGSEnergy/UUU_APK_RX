uuu (Universal Update Utility)
------------------------------
  uuu is used to program the COM boards. The Windows version
  of this utility is included in this bundle. If you want the
  latest version or a version for Linux, you can download it
  from NXP's GitHub repository:

  https://github.com/NXPmicro/mfgtools/releases
  
  Instructions
  ------------
  1. Connect the board to the PC via a USB cable
  2. Make sure the board is in OTG boot mode
  3. Put the uuu utility in the same directory as this README.txt
     file. 
  4. In Windows open a command prompt and then run uuu with a script
     file as input, such as below
     
     > uuu.exe full_tar.uuu

     If successful you will see the output Done in the terminal application.
     
Create spl_and_uboot.bin
------------------------
When using both SPL+u-boot.img it isn't possible to flash these
using u-boot FB (fastboot) since it isn't possible to specify
an offset for u-boot.img. One way to overcome this is to combine
SPL and u-boot.img into one binary file where u-boot.img is 
located at the correct offset. This can be done in Linux using dd:

  $ dd if=SPL of=spl_and_uboot.bin bs=1024
  $ dd if=u-boot.img of=spl_and_uboot.bin bs=1024 seek=68

u-boot.img should be at an offset of 69K, but we are using
seek=68 since fastboot in u-boot will skip the first 1K.

Build details
-------------
Date:     2019-12-20
meta-ea:  ea-4.14.78, 0e05eccd4dea7a32c1180658e375bf7517d99a36
