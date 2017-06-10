FROM ubuntu:16.04

RUN apt-get -y update
RUN apt-get install -y cmake g++ autoconf qt4-dev-tools patch libtool make git

# for add-apt-repository, used to get repo for newer boost version
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository --yes ppa:boost-latest/ppa
RUN apt-get update

# install dependencies
RUN apt-get install -qq libsvm-dev libglpk-dev libzip-dev zlib1g-dev libxerces-c-dev libbz2-dev
RUN apt-get install -qq libboost-date-time1.54-dev \
                        libboost-iostreams1.54-dev \
                        libboost-regex1.54-dev \
                        libboost-math1.54-dev \
                        libboost-random1.54-dev


RUN git clone https://github.com/OpenMS/contrib.git
RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=SEQAN ../contrib
RUN cmake -DBUILD_TYPE=WILDMAGIC ../contrib
RUN cmake -DBUILD_TYPE=EIGEN ../contrib


