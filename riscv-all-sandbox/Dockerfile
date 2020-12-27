FROM riscv64
MAINTAINER amaneuehara

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
WORKDIR /root
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN rm -r /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y tzdata locales
RUN apt-get install -y language-pack-ja-base language-pack-ja
RUN locale-gen ja_JP.UTF-8
ENV LANG ja_JP.UTF-8

RUN apt-get install -y git gnutls-bin
RUN git config --global user.name  "amane-uehara" && \
    git config --global user.email "62415046+amane-uehara@users.noreply.github.com"

RUN apt-get install -y zsh vim tmux wget
RUN cd $HOME                   && git clone https://github.com/amane-uehara/dotfiles.git             && \
    cd $HOME/dotfiles          && git remote set-url origin git@github.com:amane-uehara/dotfiles.git && \
    cd $HOME/dotfiles/localenv && git clone https://github.com/amane-uehara/zsh-simple-snippet.git   && \
    cd $HOME/dotfiles/localenv && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git && \
    cd $HOME                   && sh $HOME/dotfiles/install.sh

RUN cd $HOME && \
    git clone https://github.com/michaeljclark/riscv-probe.git && \
    cd $HOME/riscv-probe && \
    git remote set-url origin git@github.com:michaeljclark/riscv-probe.git

RUN cd $HOME && \
    git clone https://github.com/mit-pdos/xv6-riscv.git && \
    cd $HOME/xv6-riscv && \
    git remote set-url origin git@github.com:mit-pdos/xv6-riscv.git

RUN apt-get install -y cargo
RUN cd $HOME && git clone https://github.com/d0iasm/rvemu.git
RUN cd $HOME/rvemu && git remote set-url origin git@github.com:d0iasm/rvemu.git
RUN cd $HOME/rvemu && make rvemu-cli

RUN rm $HOME/qemu-4.2.1.tar.xz

#RUN cd $HOME && \
#    git clone https://github.com/amane-uehara/riscv-sandbox.git && \
#    cd $HOME/riscv-sandbox && \
#    git remote set-url origin git@github.com:amane-uehara/riscv-sandbox.git
