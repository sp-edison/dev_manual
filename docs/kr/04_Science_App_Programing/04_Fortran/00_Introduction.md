# Fortran 언어
## 리눅스에서 gcc로 fortran언어 컴파일하기

fortran 언어의 경우에도 gcc 컴파일러를 사용해 소스코드를 빌드할 수 있습니다. ```gfortran``` 명령어를 사용하며, C언어 빌드와 방식이 유사합니다.
포트란 언어도 역시 make 명령어를 통해 빌드하는것이 효과적입니다.

> 본 개발자 문서에서는 Makefile을 통해 C,Fortran 코드를 빌드 할 수 있는 예제 소스를 제공하고 있습니다.

## gfortran 컴파일러

EDISON 서버에 기본으로 설치되어 있는 gcc version 4.4.7 버전입니다. ```gfortran -v``` 명령어를 통해 버전을 확인할 수 있습니다.

```bash
[edison@edison ~]$ gfortran -v
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
gcc/5.3.0               intel/201 8-mpi          octave/4.0.3
gcc/5.4.0               intel/intel_11          openmpi/2.1.2
[edison@bulb ~]$ module load gcc/5.3.0
[edison@bulb ~]$ gfortran -v
Using built-in specs.
COLLECT_GCC=gfortran
COLLECT_LTO_WRAPPER=/SYSTEM/gcc-5.3.0/build/bin/../libexec/gcc/x86_64-unknown-linux-gnu/5.3.0/lto-wrapper
Target: x86_64-unknown-linux-gnu
Configured with: ./configure --prefix=/SYSTEM_BULB/gcc-5.3.0/build
Thread model: posix
gfortran version 5.3.0 (GCC)
[edison@bulb ~]$
```
