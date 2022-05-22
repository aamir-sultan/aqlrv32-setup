# aqlrv32-setup
aqlrv32 core setup documentation and First run!

## Getting started

Set your Paths:
<!-- mkdir -p ~/proj/tools; -->
Add the following paths to your .bashrc file in ~:

```shell
export PATH=$HOME/proj/binaries/riscv-toolchain/bin:$PATH
export RISCV_PATH="$HOME/proj/binaries/riscv-toolchain"
export RISCV_TOOLCHAIN=$RISCV_PATH
export RISCV_GCC="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-gcc"
export RISCV_OBJCOPY="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objcopy"
export RISCV_LD="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-ld"
export RISCV_OBJDUMP="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objdump"
export SPIKE_PATH=$RISCV_TOOLCHAIN/bin
```

or run the following command:

```shell
echo 'export PATH=$HOME/proj/binaries/riscv-toolchain/bin:$PATH
export RISCV_PATH="$HOME/proj/binaries/riscv-toolchain"
export RISCV_TOOLCHAIN=$RISCV_PATH
export RISCV_GCC="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-gcc"
export RISCV_OBJCOPY="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objcopy"
export RISCV_LD="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-ld"
export RISCV_OBJDUMP="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objdump"
export SPIKE_PATH=$RISCV_TOOLCHAIN/bin' >> ~/.bashrc
```

```shell
source ~/.bashrc
```

***

## Setting up Toolchain

```shell
mkdir -p ~/proj/tools; cd ~/proj; mkdir -p binaries/riscv-toolchain; cd tools;
```

```shell
git clone https://github.com/riscv/riscv-gnu-toolchain
```

 __For Ubuntu__

```shell
sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev
```
```shell
sudo apt-get -y install python3-pip
```
<!-- ``git clone https://github.com/riscv/riscv-gnu-toolchain`` -->
```shell
cd riscv-gnu-toolchain; mkdir build; cd build
```
```shell
../configure --prefix=$RISCV_PATH  --enable-multilib
```
```shell
make
```

Wait for a while it will take sometime to build up.

***
## Lcov setup
```shell
cd ~/proj/tools/
```

```shell
git clone https://github.com/linux-test-project/lcov.git
```

```shell
sudo make install
```

***
## Verilator Setup
### Installing Verilator
#### Prerequisites:

```shell
sudo apt-get install git perl python3 make autoconf g++ flex bison ccache
```

```shell
sudo apt-get install libgoogle-perftools-dev numactl perl-doc
```
Ubuntu only (ignore if gives error)
```shell
sudo apt-get install libfl2
``` 


Ubuntu only (ignore if gives error)
```shell
sudo apt-get install libfl-dev
```

Ubuntu only (ignore if gives error)
```shell
sudo apt-get install zlibc zlib1g zlib1g-dev
```

Only first time
```shell
git clone https://github.com/verilator/verilator
```   

***
### **Every time you need to build:**

For csh; ignore error if on bash
```shell
unsetenv VERILATOR_ROOT
```         

For bash
```shell
unset VERILATOR_ROOT
```            


```shell
cd ~/proj/tools/; cd verilator;
```

Make sure git repository is up-to-date
```shell
git pull
```                        
<!-- git tag v4.222                  # See what versions exist -->

Use development branch (e.g. recent bug fixes)
```shell
git checkout master
```            
Use most recent stable release
```shell
git checkout stable
```            
<!-- #git checkout v{version}        # Switch to specified release version -->

Create ./configure script
```shell
autoconf
```         
Configure and create Makefile
```shell
./configure
```      

```shell
make -j "nproc"
```  
Build Verilator itself (if error, try just `make`)

```shell
sudo make install
```

```shell
make test
```

***
## Cloning the Core

`mkdir -p ~/proj/cores/; cd ~/proj/cores/;`

`git clone https://github.com/aamir-sultan/aqlrv32.git`

***
### **Setup and First Run**
Only first time
```shell
source ~/.bashrc
```  

```shell
make verilator=1 all
```

Wait for the run to complete. If everything is working fine then the run will be completed sucessfully.

For further details on the core one can refer to 
```shell
https://github.com/aamir-sultan/aqlrv32.git
```


