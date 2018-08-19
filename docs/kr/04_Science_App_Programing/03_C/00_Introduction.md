# C 언어
## 리눅스에서 gcc로 c언어 컴파일하기

리눅스에서 hello world를 출력하는 간단한 C 코드를 컴파일 하고 실행하는 예제 링크 입니다.
[리눅스에서 gcc로 c언어 컴파일하기](http://ibabo.tistory.com/87)

간단한 코드의 경우 gcc 명령어를 바로 사용하여 빌드 할 수 있습니다. 하지만 소스코드가 많은 경우 일일이 gcc 명령어를 통해 컴파일 하는것은 무리가 있습니다. make 명령어를 사용하면 효과적으로 소스코드를 빌드 할 수 있습니다.

[make를 이용한 빌드 방법](http://snowdeer.github.io/c++/2017/09/06/how-to-use-make-utility/)

> 본 개발자 문서에서는 Makefile을 통해 C,Fortran 코드를 빌드 할 수 있는 예제 소스를 제공하고 있습니다.

## gcc 컴파일러

EDISON 서버에 기본으로 설치되어 있는 gcc version은 4.4.7 입니다. ```gcc -v``` 명령어를 통해 버전을 확인할 수 있습니다.




```bash
[edison@edison ~]$ gcc -v
Using built-in specs.
Target: x86_64-redhat-linux
Configured with: ../configure --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --with-bugurl=http://bugzilla.redhat.com/bugzilla --enable-bootstrap --enable-shared --enable-threads=posix --enable-checking=release --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --enable-languages=c,c++,objc,obj-c++,java,fortran,ada --enable-java-awt=gtk --disable-dssi --with-java-home=/usr/lib/jvm/java-1.5.0-gcj-1.5.0.0/jre --enable-libgcj-multifile --enable-java-maintainer-mode --with-ecj-jar=/usr/share/java/eclipse-ecj.jar --disable-libjava-multilib --with-ppl --with-cloog --with-tune=generic --with-arch_32=i686 --build=x86_64-redhat-linux
Thread model: posix
gcc version 4.4.7 20120313 (Red Hat 4.4.7-18) (GCC)
```

그 외 버전이 필요한 경우 ```module avail``` 명령어를 통해 이용 가능한 gcc 리스트를 확인하고, ```module load gcc/[버전]``` 명렁어를 통해 사용할 수 있습니다.


```bash
[edison@bulb etc]# module avail
-------------------------------------- /usr/share/Modules/modulefiles --------------------------------------
dot         module-git  module-info modules     null        use.own

--------------------------------------------- /etc/modulefiles ---------------------------------------------
R/3.3.2                 gcc/5.5.0               intel/mkl               openmpi-1.8-x86_64
R/3.3.3(default)        gnuplot/4.6.3           mpi/gnu/openmpi-1.6.5   openmpi-x86_64
gamess/gamess           gnuplot/5.0.6(default)  mpi/intel/mpich-1.2.7p1 petsc/3.9.3
gcc/4.9.4               intel/2018              mpich-x86_64            python/3.6.3
gcc/5.3.0               intel/2018-mpi          octave/4.0.3
gcc/5.4.0               intel/intel_11          openmpi/2.1.2
[edison@bulb ~]$ module load gcc/5.3.0
[edison@bulb ~]$ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/SYSTEM/gcc-5.3.0/build/bin/../libexec/gcc/x86_64-unknown-linux-gnu/5.3.0/lto-wrapper
Target: x86_64-unknown-linux-gnu
Configured with: ./configure --prefix=/SYSTEM_BULB/gcc-5.3.0/build
Thread model: posix
gcc version 5.3.0 (GCC)
[edison@bulb ~]$
```
