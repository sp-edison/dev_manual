# SIESTA 4.0.1 install (with mpich)


- [공식 홈페이지](https://www.icmab.es/siesta)
- [Documentation: Installation](https://web.pa.msu.edu/people/tomanek/SIESTA-installation.html)
- [Download 4.0.1](https://launchpad.net/siesta/4.0/4.0.1/+download/siesta-4.0.1.tar.gz)


## 필요한 모듈 로드

```bash
$ module load gcc/5.3.0
```
 > 5.3.0 버전에선  일부 lib을 못찾는다는 관련 에러 바생 -> 5.4.0으로 변경


## 설치 순서

 - 0) Gcc 5.4.0
 - 1) openmpi 3.1.1
   - 1.1) BLACS
 - 2) BLAS
   - 2.1) LAPACK
 - 3) SCALAPACK
 - 4) Siesta


### gcc 5.4.0

```bash
cd /SYSTEM/gcc
mkdir download
cd download
wget https://ftp.gnu.org/gnu/gcc/gcc-5.4.0/gcc-5.4.0.tar.gz
tar -xvf gcc-gcc-5.4.0.tar.gz
mkdir obj
cd obj
../gcc-gcc-5_4_0-release/configure --prefix=/SYSTEM/gcc/5.4.0 --with-system-zlib --enable-languages=c,c++,fortran
make
make install
```

../gcc-5_5_0/configure --prefix=/SYSTEM/gcc/5.5.0 --with-system-zlib --enable-languages=c,c++,fortran
make -j8
maie install

### openmpi 3.1.1 (with gcc-5.3.0)

```bash
module load gcc/5.3.0
cd /SYSTEM/openmpi
mkdir 3.1.1-gcc5.3
mkdir dowload
cd download
wget https://download.open-mpi.org/release/open-mpi/v3.1/openmpi-3.1.1.tar.gz
tar -xvf openmpi-3.1.1.tar.gz
cd openmpi-3.1.1
./configure --prefix=/SYSTEM/openmpi/3.1.1-gcc5.3
make -j8
make install
```



## 소스코드 다운로드 및 압축 해제

```bash
$ cd /SYSTEM/Siesta
$ mkdir download
$ cd download
$ wget https://launchpad.net/siesta/4.0/4.0.1/+download/siesta-4.0.1.tar.gz
$ tar -xvf siesta-4.0.1.tar.gz
```
## 설치

```bash
$ cd siesta-4.0.1/Obj
$ sh ../Src/obj_setup.sh
$
```


--enable-mpi --bindir=/SYSTEM/Siesta/4.0.1 --with-PACKAGE --with-blacs=/opt/intel/mkl/10.2.6.038/lib/em64t/libmkl_blacs_lp64.a

../Src/configure --enable-mpi FC=ifort MPIFC=/opt/mpi/intel/mpich-1.2.7p1/bin/mpif90 FCFLAGS="-lmpi -mkl=parallel" LDFLAGS="-lmpi -mkl=parallel" --with-siesta-blas --with-siesta-lapack --with-blacs=/opt/intel/mkl/10.2.6.038/lib/em64t/libmkl_blacs_lp64.a --with-scalapack=/opt/intel/mkl/10.2.6.038/lib/em64t/libmkl_scalapack_lp64.a



../Src/configure --enable-mpi FCFLAGS="-lmpi -mkl=parallel" LDFLAGS="-lmpi -mkl=parallel" --with-siesta-blas --with-siesta-lapack --with-blacs=/opt/intel/Compiler/11.1/073/mkl/lib/em64t/libmkl_blacs_lp64.a --with-scalapack=/opt/intel/Compiler/11.1/073/mkl/lib/em64t/libmkl_scalapack_lp64.a
