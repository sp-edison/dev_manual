# SIESTA 4.0.1 install (with gcc5.3.0 and openmpi 2.0.2)


- [공식 홈페이지](https://www.icmab.es/siesta)
- [Documentation: Installation](https://web.pa.msu.edu/people/tomanek/SIESTA-installation.html)
- [Download 4.0.1](https://launchpad.net/siesta/4.0/4.0.1/+download/siesta-4.0.1.tar.gz)

http://blog.ksc.re.kr/12



## 필요한 모듈 로드

```bash
module load gcc/5.3.0
module load openmpi/2.1.2
```
 > 5.3.0 버전에선  일부 lib을 못찾는다는 관련 에러 바생 -> 5.4.0으로 변경


## 설치 순서

 - 1) SCALAPACK
 - 4) Siesta



### Scalapack 2.0.2

```bash
mkdir /SYSTEM/Scalapack/
cd /SYSTEM/Scalapack/
mkdir 2.0.2
mkdir download
cd dowload
wget http://www.netlib.org/scalapack/scalapack-2.0.2.tgz
cd scalapack-2.0.2
mkdir build
cd build
ccmake ../
```

ccmake 설정에서 아래 두개의 설정을 다음과 같이 변경
```bash
BUILD_SHARED_LIBS                ON
CMAKE_INSTALL_PREFIX             /SYSTEM/Scalapack/2.0.2
```

```bash
make -j16
make install
```

### SIESTA 4.0.1 install (with gcc5.3.0 and openmpi 2.0.2)

```bash

cd Obj
bash ../Src/obj_setup.sh
../Src/configure --with-scalapack=/SYSTEM/Scalapack/2.0.2/lib/libscalapack.a --enable-mpi --prefix=/SYSTEM/Siesta/4.0.1
make
```


```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/SYSTEM/Scalapack/2.0.2/lib
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
