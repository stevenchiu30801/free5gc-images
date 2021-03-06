FROM golang:1.12.9

MAINTAINER steven30801@gmail.com

COPY setup.sh /root
RUN chmod 777 /root/setup.sh

ARG REPO=free5gc-stage-2
ARG TAG=v2.0.2

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        git \
        gcc \
        cmake \
        autoconf \
        libtool \
        pkg-config \
        libmnl-dev \
        libyaml-dev \
        automake \
        iptables \
        ethtool && \
    apt-get clean

ENV GOROOT=/usr/local/go
ENV GO111MODULE=off

RUN git clone https://bitbucket.org/free5GC/$REPO.git $GOPATH/src/free5gc

WORKDIR $GOPATH/src/free5gc

RUN git checkout $TAG

RUN ./install_env.sh

RUN tar -C $GOPATH -zxvf free5gc_libs.tar.gz

RUN find src/udm -type f -print0 | xargs -0 sed -i "s/Adrr/Addr/g"

RUN ./build.sh
