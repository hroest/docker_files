# Concatenated script to build OpenMS
# 
#  - downloads the OpenMS dependencies to /contrib and builds them in the
#    folder /contrib-build
#
#  - downloads the OpenMS source code to /OpenMS and builds the code in the
#    folder /openms-build
#

FROM ubuntu:12.04

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


## End of dependencies, the above image should be available at
## hroest/openms_dependencies, therefore we could start here with 
## FROM hroest/openms_dependencies 

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF ../OpenMS
RUN make OpenMS


## End of library, the above image should be available at
## hroest/openms_lib, therefore we could start here with 
## FROM hroest/openms_lib 

WORKDIR /openms-build

RUN make 

