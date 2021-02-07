FROM ubuntu:20.04
MAINTAINER amaneuehara

ENV DEBIAN_FRONTEND noninteractive
ENV NUMJOBS 8
ENV HOME /root
WORKDIR /root

RUN echo 'nameserver 8.8.8.8' >> /etc/resolv.conf
RUN echo 'nameserver 8.8.4.4' >> /etc/resolv.conf

RUN apt-get update

RUN apt-get install -y \
    autoconf           \
    automake           \
    autotools-dev      \
    bc                 \
    bison              \
    bridge-utils       \
    build-essential    \
    curl               \
    flex               \
    gawk               \
    gcc                \
    gperf              \
    libc6-dev          \
    libexpat-dev       \
    libglib2.0-dev     \
    libgmp-dev         \
    libmpc-dev         \
    libmpfr-dev        \
    libpixman-1-dev    \
    libsdl1.2-dev      \
    libtool            \
    patchutils         \
    pkg-config         \
    python3            \
    texinfo            \
    uml-utilities      \
    unzip              \
    wget               \
    zlib1g-dev

ARG rootrepo="riscv-gnu-toolchain"
ARG hash="1af07f51a090ddb9e62ef26475b16503c1aa0358"
RUN cd $HOME && \
    wget https://github.com/riscv/${rootrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    mv ${rootrepo}-${hash} ${rootrepo}

ARG subrepo="riscv-binutils-gdb"
ARG hash="2cb5c79dad39dd438fb0f7372ac04cf5aa2a7db7"
ARG submod="riscv-binutils"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

ARG subrepo="riscv-dejagnu"
ARG hash="4ea498a8e1fafeb568530d84db1880066478c86b"
ARG submod="riscv-dejagnu"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

ARG subrepo="riscv-gcc"
ARG hash="c3911e6425f35e0722129cb30cc5ccaf3390cd75"
ARG submod="riscv-gcc"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

ARG subrepo="riscv-binutils-gdb"
ARG hash="63a44e5923c859e99d3a8799fa8132b49a135241"
ARG submod="riscv-gdb"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

ARG subrepo="riscv-glibc"
ARG hash="7395b0964db9cc4dd544926414960e9a16842180"
ARG submod="riscv-glibc"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

ARG subrepo="riscv-newlib"
ARG hash="f289cef6be67da67b2d97a47d6576fa7e6b4c858"
ARG submod="riscv-newlib"
RUN cd $HOME/${rootrepo} && \
    wget https://github.com/riscv/${subrepo}/archive/${hash}.zip && \
    unzip -q ${hash}.zip && \
    rm ${hash}.zip && \
    rmdir ${submod} && \
    mv ${subrepo}-${hash} ${submod}

RUN cd $HOME/riscv-gnu-toolchain && \
    rm -rf *.zip *.tgz && \
    ./configure --prefix=/opt/riscv32 --with-arch=rv32ia --with-abi=ilp32 && \
    make linux && \
    make clean && \
    ./configure --prefix=/opt/riscv && \
    make linux

ENV PATH /opt/riscv32/bin:$PATH
ENV PATH /opt/riscv/bin:$PATH

RUN cd $HOME && \
    wget https://download.qemu.org/qemu-4.2.1.tar.xz && \
    tar xvf ./qemu-4.2.1.tar.xz && \
    cd $HOME/qemu-4.2.1 && \
    ./configure --prefix=/opt/riscv32-qemu --target-list=riscv32-softmmu && \
    make -j4 && \
    make install && \
    make clean && \
    ./configure --prefix=/opt/riscv64-qemu --target-list=riscv64-softmmu && \
    make -j4 && \
    make install

ENV PATH /opt/riscv32-qemu/bin:$PATH
ENV PATH /opt/riscv64-qemu/bin:$PATH
