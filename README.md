# cross-compiler
交叉编译的一些坑


自己编译中有很多坑，例如glibc的编译，调用，gcc的链接等出现各种各样的问题，导致无法使用，折腾了一天多

试了一下这位仁兄的，发现可以，就放弃折腾了。

```bash
sudo apt-get install gcc-7-multilib-arm-linux-gnueabi -y;sudo apt-get install gcc-7-multilib-arm-linux-gnueabihf -y;sudo apt-get install gcc-7-multilib-mips64el-linux-gnuabi64 -y;sudo apt-get install gcc-7-multilib-mips64-linux-gnuabi64 -y;sudo apt-get install gcc-7-multilib-mipsel-linux-gnu -y;sudo apt-get install gcc-7-multilib-mips-linux-gnu -y;sudo apt-get install gcc-7-multilib-powerpc64-linux-gnu -y;sudo apt-get install gcc-7-multilib-powerpc-linux-gnu -y;sudo apt-get install gcc-7-multilib-s390x-linux-gnu -y;sudo apt-get install gcc-7-multilib-sparc64-linux-gnu -y



How to compile?

arm-linux-gnueabi-gcc-7 -o test test.c (arm 32bit binary)

mips-linux-gnu-gcc-7 -o test test.c (mips 32bit binary)

mips64-linux-gnuabi64-gcc-7 -o test test.c (mips 64bit binary)

powerpc-linux-gnu-gcc-7 -o test test.c (ppc 32bit binary)

powerpc64-linux-gnu-gcc-7 -o test test.c (ppc 64bit binary)

s390x-linux-gnu-gcc-7 -o test test.c (IBM S/390 64bit binary)

sparc64-linux-gnu-gcc-7 -o test test.c (SPARC V9 64bit binary)



How to excution?

sudo apt-get install qemu-user-static

```
在编译库的时候需要指定编译器，才能编译成功/(ㄒoㄒ)/~~

```
export CC=/usr/bin/powerpc-linux-gnu-gcc-7
export CC=/usr/bin/mips-linux-gnu-gcc-7
export CC=/usr/bin/arm-linux-gnueabi-gcc
```

为了更好的测试，编译的时候需要使用静态链接
```
./configure --host arm-linux-gnueabi --enable-shared=no --enable-static=yes
```
--enable-shared=no --enable-static=yes对于coreutils似乎无效于是直接在makefile里的CFLAGS直接添加'-static'



