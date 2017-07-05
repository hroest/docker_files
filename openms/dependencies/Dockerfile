FROM ubuntu:14.04

# Metadata
LABEL base.image="openms_dependencies"
LABEL version="2.0"
LABEL software="OpenMS (dependencies)"
LABEL software.version="2.2.0-small"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

RUN sudo apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf patch libtool make git && \
         apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# fix to get cmake 3.x in ubuntu 14.04
RUN add-apt-repository ppa:george-edison55/cmake-3.x
RUN sudo apt-get -y update && \
         apt-get install -y cmake && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install dependencies
## TODO: --no-install-suggests
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

RUN git clone https://github.com/OpenMS/contrib.git && rm -rf contrib/.git/
RUN mkdir contrib-build

# forgot automake ! 
RUN sudo apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ automake && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /contrib-build

RUN cmake -DBUILD_TYPE=SEQAN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=WILDMAGIC ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=EIGEN ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=COINOR ../contrib && rm -rf archives src
RUN cmake -DBUILD_TYPE=SQLITE ../contrib && rm -rf archives src

# install dependencies
RUN sudo apt-get -y update && \
         apt-get install -y cmake && \
         apt-get install -y --no-install-recommends --no-install-suggests qt4-dev-tools qt4-default qt4-qtconfig qt4-qmake && \
         apt-get install -y --no-install-recommends --no-install-suggests libqt4-dev libqt4-opengl-dev libqt4-svg && \
         apt-get install -y --no-install-recommends --no-install-suggests libqt4-webkit libqtwebkit-dev && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

