# aqlrv32-setup
aqlrv32 core setup documentation and First run!
## aqlrv32-setup

## Getting started

Set your Paths:
<!-- mkdir -p ~/proj/tools; -->
Add the following paths to your .bashrc file in ~:

`export PATH=$HOME/proj/binaries/riscv-toolchain/bin:$PATH
export RISCV_PATH="$HOME/proj/binaries/riscv-toolchain"
export RISCV_TOOLCHAIN=$RISCV_PATH
export RISCV_GCC="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-gcc"
export RISCV_OBJCOPY="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objcopy"
export RISCV_LD="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-ld"
export RISCV_OBJDUMP="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objdump"
export SPIKE_PATH=$RISCV_TOOLCHAIN/bin`

or run the following command:

`echo 'export PATH=$HOME/proj/binaries/riscv-toolchain/bin:$PATH
export RISCV_PATH="$HOME/proj/binaries/riscv-toolchain"
export RISCV_TOOLCHAIN=$RISCV_PATH
export RISCV_GCC="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-gcc"
export RISCV_OBJCOPY="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objcopy"
export RISCV_LD="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-ld"
export RISCV_OBJDUMP="$RISCV_TOOLCHAIN/bin/riscv64-unknown-elf-objdump"
export SPIKE_PATH=$RISCV_TOOLCHAIN/bin' >> ~/.bashrc`

`source ~/.bashrc`

***

## Setting up Toolchain

`mkdir -p ~/proj/tools; cd ~/proj; mkdir -p binaries/riscv-toolchain; cd tools;`

``git clone https://github.com/riscv/riscv-gnu-toolchain``

 __For Ubuntu__

``sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev``
``sudo apt-get -y install python3-pip``
<!-- ``git clone https://github.com/riscv/riscv-gnu-toolchain`` -->
``cd riscv-gnu-toolchain; mkdir build; cd build``
``../configure --prefix=$RISCV_PATH  --enable-multilib``
``make``

Wait for a while it will take sometime to build up.

***
## Lcov setup
``cd ~/proj/tools/`

`git clone https://github.com/linux-test-project/lcov.git`

`sudo make install`

***
## Verilator Setup
### Installing Verilator
#### Prerequisites:

`sudo apt-get install git perl python3 make autoconf g++ flex bison ccache`

`sudo apt-get install libgoogle-perftools-dev numactl perl-doc`

`sudo apt-get install libfl2`  # Ubuntu only (ignore if gives error)

`sudo apt-get install libfl-dev`  # Ubuntu only (ignore if gives error)

`sudo apt-get install zlibc zlib1g zlib1g-dev`  # Ubuntu only (ignore if gives error)

`git clone https://github.com/verilator/verilator`   # Only first time

***
#### Every time you need to build:

`unsetenv VERILATOR_ROOT`         # For csh; ignore error if on bash

`unset VERILATOR_ROOT`            # For bash

`cd ~/proj/tools/; cd verilator;`

`git pull`                        # Make sure git repository is up-to-date
<!-- git tag v4.222                  # See what versions exist -->

`git checkout master`            # Use development branch (e.g. recent bug fixes)

`git checkout stable`            # Use most recent stable release
<!-- #git checkout v{version}        # Switch to specified release version -->


`autoconf`         # Create ./configure script

`./configure`      # Configure and create Makefile

`make -j "nproc"`  # Build Verilator itself (if error, try just `make`)

`sudo make install`

`make test`

***
## Cloning the Core

`mkdir -p ~/proj/cores/; cd ~/proj/cores/;`

`git clone https://github.com/aamir-sultan/aqlrv32.git`

***
### Setup and First Run

`source ~/.bashrc`  # Only first time

`make verilator=1 all`

Wait for the run to complete. If everything is working fine then the run will be completed sucessfully.

For further details on the core one can refer to `https://github.com/aamir-sultan/aqlrv32.git`


