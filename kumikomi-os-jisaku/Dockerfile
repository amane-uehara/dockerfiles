# https://github.com/kjmatu/12step_self_embedded_os_dev_enviroment
FROM ubuntu:20.04
LABEL description="gcc for H8"
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
# build-essential(gcc etc) install
RUN apt-get update \
    && apt-get install -y \
        autogen \
        build-essential \
        libgmp-dev \
        libmpfr-dev \
        libmpc-dev \
        unzip \
        wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# download and build binutils for h8300
WORKDIR /home/h8300-tools
RUN wget https://ftp.gnu.org/gnu/binutils/binutils-2.30.tar.gz \
    && tar zxvf binutils-2.30.tar.gz \
    && rm binutils-2.30.tar.gz
WORKDIR /home/h8300-tools/binutils-build
RUN ./../binutils-2.30/configure \
        --prefix=/usr/local \
        --target=h8300-elf \
    && make \
    && make install

# download and build gcc for h8300
WORKDIR /home/h8300-tools/
RUN wget https://ftp.gnu.org/gnu/gcc/gcc-7.3.0/gcc-7.3.0.tar.gz \
    && tar zxvf gcc-7.3.0.tar.gz \
    && rm gcc-7.3.0.tar.gz
WORKDIR /home/h8300-tools/gcc-build
RUN ./../gcc-7.3.0/configure \
        --disable-libstdcxx-pch \
        --disable-libssp \
        --disable-nls \
        --disable-shared \
        --disable-threads \
        --enable-gold \
        --enable-languages=c \
        --enable-lto \
        --enable-sjlj-exceptions \
        --prefix=/usr/local \
        --target=h8300-elf \
        --with-gmp=/usr/local \
        --with-mpfr=/usr/local \
        --with-mpc=/usr/local \
        --disable-bootstrap \
    && make \
    && make check \
    && make install

ENV PATH $PATH:/usr/local/h8300-elf/bin

WORKDIR /home
RUN wget http://kozos.jp/kozos/osbook/osbook_03.zip \
    && unzip osbook_03.zip \
    && rm osbook_03.zip

RUN rm -rf /home/h8300-tools

# ----------------------------------------------------------------------------------------------------

RUN apt-get update && \
    apt-get install -y \
    git \
    gnutls-bin \
    language-pack-ja \
    language-pack-ja-base \
    locales \
    tmux \
    tzdata \
    vim \
    wget \
    zsh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN locale-gen ja_JP.UTF-8
ENV LANG ja_JP.UTF-8

RUN git config --global user.name  "amane-uehara" && \
    git config --global user.email "62415046+amane-uehara@users.noreply.github.com"

RUN cd $HOME                   && git clone https://github.com/amane-uehara/dotfiles.git             && \
    cd $HOME/dotfiles          && git remote set-url origin git@github.com:amane-uehara/dotfiles.git && \
    cd $HOME/dotfiles/localenv && git clone https://github.com/amane-uehara/zsh-simple-snippet.git   && \
    cd $HOME/dotfiles/localenv && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git && \
    cd $HOME                   && sh $HOME/dotfiles/install.sh
