FROM python:3.6-slim-buster
MAINTAINER amaneuehara

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /opt
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apt-get update --fix-missing && apt-get install -y \
    tzdata \
    locales \
    curl \
    git \
    vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/orcasgit/python-fitbit.git
RUN cd python-fitbit && pip3 install -r requirements/base.txt
RUN cd python-fitbit && pip3 install -r requirements/dev.txt
RUN cd python-fitbit && pip3 install -r requirements/test.txt
RUN cd python-fitbit && pip3 install cherrypy
RUN cd python-fitbit && pip3 install fitbit
