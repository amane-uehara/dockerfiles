FROM ubuntu:20.04
MAINTAINER amaneuehara
ENV DEBIAN_FRONTEND noninteractive
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

WORKDIR /opt

RUN apt-get update \
    && apt-get install -y \
    bison \
    build-essential \
    clang \
    cmake \
    flex \
    g++ \
    gawk \
    git \
    graphviz \
    libboost-all-dev \
    libboost-dev \
    libboost-filesystem-dev \
    libboost-iostreams-dev \
    libboost-program-options-dev \
    libboost-python-dev \
    libboost-system-dev \
    libboost-thread-dev \
    libeigen3-dev \
    libffi-dev \
    libftdi-dev \
    libftdi1 \
    libreadline-dev \
    pkg-config \
    python3-dev \
    tcl-dev \
    xdot \
    zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/YosysHQ/icestorm.git \
    && cd icestorm \
    && export CPPFLAGS="-I/usr/include/libftdi1 -I/usr/include/libusb-1.0" \
    && make -j4 \
    && make install \
    && cd .. \
    && rm -rf icestorm

RUN git clone https://github.com/YosysHQ/nextpnr.git \
    && cd nextpnr \
    && cmake -DARCH=ice40 -DCMAKE_INSTALL_PREFIX=/usr/local . \
    && make -j4 \
    && make install \
    && cd .. \
    && rm -rf nextpnr

RUN git clone https://github.com/YosysHQ/yosys.git \
    && cd yosys \
    && make -j4 \
    && make install \
    && cd .. \
    && rm -rf yosys

RUN apt-get autoremove --purge -y \
    bison \
    build-essential \
    clang \
    cmake \
    flex \
    g++ \
    gawk \
    pkg-config \
    && apt-get clean

RUN git clone https://github.com/master-q/cpubook-code \
    && cd cpubook-code \
    && git checkout feature/support-yosys-icestick


#    python3-dev \
#    graphviz \
#    git \
#    libboost-all-dev \
#    libboost-dev \
#    libboost-filesystem-dev \
#    libboost-iostreams-dev \
#    libboost-program-options-dev \
#    libboost-python-dev \
#    libboost-system-dev \
#    libboost-thread-dev \
#    libeigen3-dev \
#    libffi-dev \
#    libftdi-dev \
#    libftdi1 \
#    libreadline-dev \
#    tcl-dev \
#    zlib1g-dev
#    xdot \
