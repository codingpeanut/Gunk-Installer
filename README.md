# stlink-v2 flash gunk  

## Preparation  
### Compile Firmware
1. install wsl
```powershell
wsl --install
```
2. compile `gnuk-vidpid.bin`
```bash
sudo apt-get install gcc-arm-none-eabi picolibc-arm-none-eabi make
git clone git://git.gniibe.org/gnuk/gnuk.git
cd gnuk/
git submodule update --init
cd src/
export kdf_do=optional
./configure --enable-factory-reset --target=ST_DONGLE --vidpid=234b:0000 --enable-certdo
make build/gnuk-vidpid.bin
```

### Driver
1. install `driver\en.stsw-link009\dpinst_amd64.exe` or `driver\en.stsw-link009\dpinst_x86.exe` depends on your system arch

### Use STM32 ST-LINK Utility to Remove Read Out Protection
1. install `driver\en.stsw-link004\STM32 ST-LINK Utility v4.6.0\setup.exe`
2. launch `STM32 ST-LINK Utility` from your computer
3. select `Target > Option Bytes > Read Out Protection > Disabled`

### Modify `stm32f1x.cfg`
1. open `bin\OpenOCD-20231002-0.12.0\share\openocd\scripts\target\stm32f1x.cfg`
2. replace `set _CPUTAPID 0x1ba01477` with `set _CPUTAPID 0x2ba01477`

## Install Gunk
1. execute `bin\start-openocd.bat`
2. execute `bin\enable-telnet.bat`
3. execute `bin\flash-gunk.bat`
4. DONE

## Resources
https://tccmu.com/2024/08/05/gnuk/
https://blog.csdn.net/nick_young_qu/article/details/108217987
https://salsa.debian.org/gnuk-team/gnuk/gnuk