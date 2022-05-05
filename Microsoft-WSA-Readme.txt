1. Install a Ubuntu 18.04 distribution or Install Ubuntu 18.04 in WSL

2. sudo install build-essential flex bison libssl-dev libelf-dev git gcc curl make bc bison ca-certificates gnupg libelf-dev lsb-release software-properties-common wget libncurses-dev binutils-aarch64-linux-gnu gcc-aarch64-linux-gnu 

3. Setup LLVM
wget https://apt.llvm.org/llvm.sh 
chmod +x llvm.sh 
sudo ./llvm.sh $LLVM_VERSION 
rm ./llvm.sh 
sudo ln -s --force /usr/bin/clang-$LLVM_VERSION /usr/bin/clang 
sudo ln -s --force /usr/bin/ld.lld-$LLVM_VERSION /usr/bin/ld.lld 
sudo ln -s --force /usr/bin/llvm-objdump-$LLVM_VERSION /usr/bin/llvm-objdump 
sudo ln -s --force /usr/bin/llvm-ar-$LLVM_VERSION /usr/bin/llvm-ar 
sudo ln -s --force /usr/bin/llvm-nm-$LLVM_VERSION /usr/bin/llvm-nm 
sudo ln -s --force /usr/bin/llvm-strip-$LLVM_VERSION /usr/bin/llvm-strip 
sudo ln -s --force /usr/bin/llvm-objcopy-$LLVM_VERSION /usr/bin/llvm-objcopy 
sudo ln -s --force /usr/bin/llvm-readelf-$LLVM_VERSION /usr/bin/llvm-readelf 
sudo ln -s --force /usr/bin/clang++-$LLVM_VERSION /usr/bin/clang++ 

4. Build the kernel

 - # Build ARM64 kernel
    $cp configs/arm64/kernel_defconfig $KERNEL_ROOT/.config 
    $make -j$(nproc) LLVM=1 ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu Image 
    After compilation you can find the compiled version at the following location: arch/arm64/boot/Image

- # Build x86_64 kernel 
    $cp configs/x86_64/kernel_defconfig $KERNEL_ROOT/.config 
    $make -j$(nproc) LLVM=1 bzImage 
    After compilation you can find the compiled version at the following location: arch/x86/boot/bzImage
