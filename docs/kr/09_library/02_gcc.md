
```bash
#!/bin/bash

# this script installs GCC 5.4.0
# to use it navigate to your home directory and type:
# sh install-gcc-5.4.0.sh

# download and install gcc 4.9.3
wget https://github.com/gcc-mirror/gcc/archive/gcc-5_4_0-release.tar.gz
tar xzf gcc-5_4_0-release.tar.gz
cd gcc-5_4_0-release
./contrib/download_prerequisites
cd ..
mkdir objdir

cd objdir
../gcc-5_4_0-release/configure --prefix=$HOME/gcc-5.4.0 --disable-nls --enable-languages=c,c++ --with-ld=/bin/ld --with-nm=/bin/nm --with-as=/usr/bin/as --disable- multilib
make

# install
make install

# clean up
rm -rf ~/objdir
rm -f ~/gcc-5_4_0-release.tar.gz


# add to path (you may want to add these lines to $HOME/.bash_profile)
export PATH=$HOME/gcc-5.4.0/bin:$PATH
export LD_LIBRARY_PATH=$HOME/gcc-5.4.0/lib:$HOME/gcc-5.4.0/lib64:$LD_LIBRARY_PATH
```


/SYSTEM/gcc/gcc-gcc-5_4_0-release
이동후

make install
