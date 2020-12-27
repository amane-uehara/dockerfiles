FROM ubuntu20.04-rv32ia-single
MAINTAINER amaneuehara

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
WORKDIR /root
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

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

RUN apt-get install -y cargo
RUN cd $HOME && \
    git clone https://github.com/d0iasm/rvemu.git && \
    cd rvemu && \
    make rvemu-cli
