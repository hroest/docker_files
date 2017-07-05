# Base Image
FROM ubuntu:14.04

# Metadata
LABEL base.image="openms_dependencies:qt5"
LABEL version="1.1"
LABEL software="OpenMS (dependencies)"
LABEL software.version="devel"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

# Maintainer
MAINTAINER Hannes Rost <hroest@stanford.edu>

USER root

# Install Step 1: basic dependencies
RUN sudo apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf patch libtool make git automake && \
         apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 2: obtain cmake 3.x in ubuntu 14.04
RUN add-apt-repository ppa:george-edison55/cmake-3.x
RUN sudo apt-get -y update && \
         apt-get install -y cmake && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 3: advanced dependencies
RUN sudo apt-get -y update && \
         apt-get install -y cmake && \
         apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev libglpk-dev libzip-dev zlib1g-dev libxerces-c-dev libbz2-dev && \
         apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.54-dev \
                                 libboost-iostreams1.54-dev \
                                 libboost-regex1.54-dev \
                                 libboost-math1.54-dev \
                                 libboost-random1.54-dev && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 4: Qt5
RUN add-apt-repository ppa:beineri/opt-qt571-trusty 
RUN sudo apt-get -y update && \
         apt-get install -y qt57base qt57webengine qt57svg libgl1-mesa-dev && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Step 5: Compiled dependencies
RUN git clone https://github.com/OpenMS/contrib.git && rm -rf contrib/.git/
RUN mkdir contrib-build

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=SEQAN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=WILDMAGIC ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=EIGEN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=COINOR ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=SQLITE ../contrib && rm -rf archives src

WORKDIR /
