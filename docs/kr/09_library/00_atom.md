

# Atom 4.2.7_2 Install

설치 순서
 - xmlf90-1.5.3 설치
 - libgridxc-0.8.0 설치
    - libxc-4.2.3 설치
 - atom-4.2.7_2 설치

 ```bash
 [edison SYSTEM]$ module load gcc/4.9.3
 [edison SYSTEM]$ mkdir /SYSTEM/atom/util
 [edison SYSTEM]$ mkdir /SYSTEM/atom/download
 [edison SYSTEM]$ cd atom/
 [edison SYSTEM]$ mkdir 4.2.7_2
 [edison SYSTEM]$ mkdir 4.2.7_2/bin
 [edison atom]$ mkdir download
 ```

## 1. xmlf90-1.5.3 설치

- [공식 홈페이지](https://launchpad.net/xmlf90)
- [xmlf90-1.5.3 download](https://launchpad.net/xmlf90/trunk/1.5/+download/xmlf90-1.5.3.tar.gz)

Install
```bash
[edison download]$ tar xvf xmlf90-1.5.3.tar.gz
[edison download]$ cd xmlf90-1.5.3
[edison xmlf90-1.5.3]$ mkdir /SYSTEM/atom/util/xmlf90-1.5.4
[edison xmlf90-1.5.3]$ ./configure --prefix=/SYSTEM/atom/util/xmlf90-1.5.4
[edison xmlf90-1.5.3]$ make -j8
[edison xmlf90-1.5.3]$ make install
[edison xmlf90-1.5.3]$ ls /SYSTEM/atom/util/xmlf90-1.5.4/
include  lib  share
```

## 2. libgridxc-0.8.0 설치


 - [공식 홈페이지](https://launchpad.net/libgridxc)
 - [libxc-4.2.3 download](https://launchpad.net/libgridxc/trunk/0.8/+download/libgridxc-0.8.0.tgz)


libgridxc-0.8.0 설치를 위해서는 libxc-4.2.3 설치가 필요

### 2.1. libxc-4.2.3 설치
 - [공식 홈페이지](http://www.tddft.org/programs/libxc/download)
 - [libxc-4.2.3 download](http://www.tddft.org/programs/octopus/down.php?file=libxc/4.2.3/libxc-4.2.3.tar.gz)

libxc-4.2.3 Install
```bash
[edison download]$ cd /SYSTEM/atom/download
[edison download]$ wget https://departments.icmab.es/leem/siesta/Pseudopotentials/Code/atom-4.2.7_2.tgz
[edison download]$ tar xvf down.php\?file\=libxc%2F4.2.3%2Flibxc-4.2.3.tar.gz
[edison download]$ cd libxc-4.2.3
[edison xmlf90-1.5.3]$ mkdir /SYSTEM/atom/util/libxc-4.2.3
[edison libxc-4.2.3]$ ./configure --prefix=/SYSTEM/atom/util/libxc-4.2.3 --enable-fortran
[edison download]$ make -j8
[edison download]$ make install
[edison libxc-4.2.3]$ ls /SYSTEM/atom/util/libxc-4.2.3/
bin  include  lib
```

### 2.2. libgridxc-0.8.0 설치

libgridxc-0.8.0 install

```bash
[edison download]$ cd /SYSTEM/atom/download
[edison download]$ tar xvf libgridxc-0.8.0.tgz
[edison download]$ cd libgridxc-0.8.0
[edison libgridxc-0.8.0]$ mkdir Gfortran
[edison libgridxc-0.8.0]$ cd Gfortran/
[edison Gfortran]$ cp ../extra/fortran.mk .
[edison libgridxc-0.8.0]$ vi fortran.mk
```

fortran.mk 파일의 LIBXC_ROOT 경로 수정

```LIBXC_ROOT=/usr/local -> LIBXC_ROOT=/SYSTEM/atom/util/libxc-4.2.3```

fortran.mk 파일 일부 내용
```
libgridxc-0.8.0/src/m_fft_gpfa.F
#
# Example Fortran macros: gfortran
#
# Make sure this variable is set if you intend to use libxc
LIBXC_ROOT=/SYSTEM/atom/util/libxc-4.2.3
#
# These two instances are needed, instead of just FC
FC_SERIAL=gfortran
FC_PARALLEL=mpif90
...
```

```
[edison Gfortran]$ make clean
[edison Gfortran]$ make PREFIX=/SYSTEM/atom/util/libgridxc-0.8.0
```


## 3. atom Install

- [Atom 공식 홈페이지](https://departments.icmab.es/leem/siesta/Pseudopotentials/Code/downloads.html)
- [Atom 4.2.7_2 download](https://departments.icmab.es/leem/siesta/Pseudopotentials/Code/atom-4.2.7_2.tgz)



/SYSTEM 폴더에 atom 폴더 생성 및 설치 atom 다운로드
``` sh
[edison atom]$ cd /SYSTEM/atom/download/
[edison download]$ wget https://departments.icmab.es/leem/siesta/Pseudopotentials/Code/atom-4.2.7_2.tgz
[edison download]$ tar xvf atom-4.2.7_2.tgz
[edison download]$ cd atom-4.2.7_2
```
arch.make 파일 수정
```
[edison atom-4.2.7_2]$ mv arch.make.sample arch.make
[edison atom-4.2.7_2]$ vi arch.make
```

주석 처리된 ```XMLF90_ROOT``` 과 ```GRIDXC_ROOT```를 위에서 설치한 경로를 지정하고 저장

```sh
XMLF90_ROOT=/SYSTEM/atom/util/xmlf90-1.5.4
GRIDXC_ROOT=/SYSTEM/atom/util/libgridxc-0.8.0
```

컴파일 및 생성된 실행파일을 복사
```
[edison atom-4.2.7_2]$ make
[edison atom-4.2.7_2]$ cp atm /SYSTEM/atom/4.2.7_2/bin
```


## 참고자료
http://personales.unican.es/junqueraj/JavierJunquera_files/Metodos/Pseudos/Siesta-abinit/Siesta-Abinit-PSML.pdf
