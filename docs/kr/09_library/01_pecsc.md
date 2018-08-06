# PETSc install (with gcc 5.3.0)


- [공식 홈페이지](https://www.mcs.anl.gov/petsc/)
- [Documentation: Installation](https://www.mcs.anl.gov/petsc/documentation/installation.html)
- [Download](https://www.mcs.anl.gov/petsc/download/index.html)



```bash
$ wget http://ftp.mcs.anl.gov/pub/petsc/release-snapshots/petsc-3.9.3.tar.gz
$ mkdir /SYSTEM/petsc/3.9.3
$ cd petsc-3.9.3
$ module load gcc/5.4.0
$ ./configure --prefix=/SYSTEM/petsc/3.9.3 --with-cc=gcc --with-cxx=g++ --with-fc=gfortran --download-mpich
$  make PETSC_DIR=/SYSTEM/petsc/petsc-3.9.3 PETSC_ARCH=arch-linux2-c-debug all
```
