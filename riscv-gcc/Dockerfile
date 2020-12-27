FROM plain:latest
MAINTAINER amaneuehara

RUN apt-get install -y \
    autoconf         \
    automake         \
    autotools-dev    \
    curl             \
    python3          \
    libmpc-dev       \
    libmpfr-dev      \
    libgmp-dev       \
    gawk             \
    build-essential  \
    bison            \
    flex             \
    texinfo          \
    gperf            \
    libtool          \
    patchutils       \
    bc               \
    zlib1g-dev       \
    libexpat-dev     \
    unzip

ENV NUMJOBS 8
ENV DOCKERFILE_IMAGE_NAME riscv-gcc

RUN wget https://github.com/riscv/riscv-gnu-toolchain/archive/1af07f51a090ddb9e62ef26475b16503c1aa0358.zip -O $HOME/riscv-gnu-toolchain.zip
RUN cd $HOME && \
    unzip -q riscv-gnu-toolchain.zip && \
    rm riscv-gnu-toolchain.zip && \
    mv riscv-gnu-toolchain-1af07f51a090ddb9e62ef26475b16503c1aa0358 riscv-gnu-toolchain

RUN wget https://github.com/riscv/riscv-binutils-gdb/archive/2cb5c79dad39dd438fb0f7372ac04cf5aa2a7db7.zip  -O $HOME/riscv-gnu-toolchain/riscv-binutils.zip
RUN wget https://github.com/riscv/riscv-dejagnu/archive/4ea498a8e1fafeb568530d84db1880066478c86b.zip       -O $HOME/riscv-gnu-toolchain/riscv-dejagnu.zip
RUN wget https://github.com/riscv/riscv-gcc/archive/c3911e6425f35e0722129cb30cc5ccaf3390cd75.zip           -O $HOME/riscv-gnu-toolchain/riscv-gcc.zip
RUN wget https://github.com/riscv/riscv-binutils-gdb/archive/63a44e5923c859e99d3a8799fa8132b49a135241.zip  -O $HOME/riscv-gnu-toolchain/riscv-gdb.zip
RUN wget https://github.com/riscv/riscv-glibc/archive/7395b0964db9cc4dd544926414960e9a16842180.zip         -O $HOME/riscv-gnu-toolchain/riscv-glibc.zip
RUN wget https://github.com/riscv/riscv-newlib/archive/f289cef6be67da67b2d97a47d6576fa7e6b4c858.zip        -O $HOME/riscv-gnu-toolchain/riscv-newlib.zip
RUN wget 'https://git.qemu.org/?p=qemu.git;a=snapshot;h=57dfc2c4d51e770ed3f617e5d1456d1e2bacf3f0;sf=tgz'   -O $HOME/riscv-gnu-toolchain/qemu.tgz

RUN cd $HOME/riscv-gnu-toolchain && \
    unzip -q riscv-binutils.zip && rm riscv-binutils.zip && \
    unzip -q riscv-dejagnu.zip  && rm riscv-dejagnu.zip  && \
    unzip -q riscv-gcc.zip      && rm riscv-gcc.zip      && \
    unzip -q riscv-gdb.zip      && rm riscv-gdb.zip      && \
    unzip -q riscv-glibc.zip    && rm riscv-glibc.zip    && \
    unzip -q riscv-newlib.zip   && rm riscv-newlib.zip   && \
    tar xfz qemu.tgz            && rm qemu.tgz

RUN cd $HOME/riscv-gnu-toolchain && \
    rmdir riscv-binutils && mv riscv-binutils-gdb-2cb5c79dad39dd438fb0f7372ac04cf5aa2a7db7 riscv-binutils && \
    rmdir riscv-dejagnu  && mv riscv-dejagnu-4ea498a8e1fafeb568530d84db1880066478c86b      riscv-dejagnu  && \
    rmdir riscv-gcc      && mv riscv-gcc-c3911e6425f35e0722129cb30cc5ccaf3390cd75          riscv-gcc      && \
    rmdir riscv-gdb      && mv riscv-binutils-gdb-63a44e5923c859e99d3a8799fa8132b49a135241 riscv-gdb      && \
    rmdir riscv-glibc    && mv riscv-glibc-7395b0964db9cc4dd544926414960e9a16842180        riscv-glibc    && \
    rmdir riscv-newlib   && mv riscv-newlib-f289cef6be67da67b2d97a47d6576fa7e6b4c858       riscv-newlib   && \
    rmdir qemu           && mv qemu-57dfc2c                                                qemu

RUN cd $HOME/riscv-gnu-toolchain && rm -rf *.zip *.tgz

#COPY riscv-gnu-toolchain /root/riscv-gnu-toolchain/
#RUN cd $HOME/riscv-gnu-toolchain && \
#    ./configure --prefix=/opt/riscv32 --with-arch=rv32i --with-abi=ilp32d && \
#    make linux
#
#ENV PATH /opt/riscv32/bin:$PATH

# ./configure --prefix=/opt/riscv32 --with-arch=rv32ia --with-abi=ilp32 -mcmodel=medany
# git clone --recursive https://github.com/riscv/riscv-gnu-toolchain


# ./configure --prefix=/opt/riscv32 --with-arch=rv32ia --with-abi=ilp32
# make linux
