[[_TOC_]]


# How to build fh_loader and QSaharaServer Linux executable
- reference: KBA-170227075252

## Build fh_loader
```
tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/fh_loader$ make
mkdir -p bin
gcc -o bin/fh_loader fh_cobs.c fh_crc.c fh_hsuart_packet.c fh_loader.c fh_loader_sha.c fh_transfer.c fh_transport.c fh_transport_com.c fh_transport_hsuart.c fh_transport_linux_pipe.c stringl/memscpy.c stringl/memsmove.c stringl/strlcat.c stringl/strlcpy.c -I./ -I./stringl/ -lrt
fh_loader.c: In function ‘file_path_add_path’:
fh_loader.c:1354:5: warning: implicit declaration of function ‘memscpy’; did you mean ‘memccpy’? [-Wimplicit-function-declaration]
 1354 |     memscpy(out_path, len, path, len);
      |     ^~~~~~~
      |     memccpy

:
fh_loader.c:10017:9: note: ‘snprintf’ output between 68 and 4450 bytes into a destination of size 2048
10017 |         snprintf (SizeString3, sizeof(SizeString3), "FILE ACCESS SLOW!! %10s in %6.3f seconds (%10sps) --- ", SizeString2, NetworkElapsed, SizeString1);
      |         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
```
tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/fh_loader$ find | grep fh_l
./bin/fh_loader
./fh_loader_sha.c
./fh_loader_sha.h
./fh_log.h
./fh_loader.c
tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/fh_loader$ cd bin/
tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/fh_loader/bin$ ./fh_loader 

Base Version: 20.06.16.20.28
Binary build date: May 10 2021 @ 18:31:26

```

## Build QSaharaServer
```
tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/QSaharaServer/src$ cmake CMakeLists.txt 
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/bin/cc
:

Scanning dependencies of target QSaharaServer
[ 14%] Building C object CMakeFiles/QSaharaServer.dir/kickstart.c.o
[ 28%] Building C object CMakeFiles/QSaharaServer.dir/sahara_protocol.c.o
[ 42%] Building C object CMakeFiles/QSaharaServer.dir/comm.c.o
:

tingkuanyu@TKubunt20:/D/c1/11/main/nonhlos/BOOT.MXF.1.0/boot_images/boot/QcomPkg/Tools/storage/fh_loader/QSaharaServer/src$ ./QSaharaServer 
Binary build date: May 10 2021 @ 18:33:51
QSAHARASERVER CALLED LIKE THIS: './QSaharaServe'Binary build date: May 10 2021 @ 18:33:51
Built May 10 2021 18:33:51
Sahara mappings:
:

```