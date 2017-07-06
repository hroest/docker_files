FROM ubuntu:17.04

# Metadata
LABEL base.image="openms_dependencies"
LABEL version="2.0"
LABEL software="OpenMS (dependencies)"
LABEL software.version="2.2.0-17.04"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

USER root

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf automake patch libtool make git && \
    apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties && \
    apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install dependencies (cmake is 3.5 in 16.04)
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-install-suggests libsvm-dev libglpk-dev libzip-dev zlib1g-dev \
                        libxerces-c-dev libbz2-dev cmake && \
    apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install boost (cmake is 3.5 in 16.04)
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-install-suggests libboost-date-time1.62-dev \
                        libboost-iostreams1.62-dev \
                        libboost-regex1.62-dev \
                        libboost-math1.62-dev \
                        libboost-random1.62-dev && \
    apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install specific dependencies
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-install-suggests libwildmagic-dev \
         coinor-libcoinutils-dev coinor-libcgl-dev coinor-libcbc-dev \
				 coinor-libclp-dev coinor-libosi-dev coinor-libvol-dev \
         seqan-dev libeigen3-dev libsqlite3-dev && \
    apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install Qt4 dependencies
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --no-install-suggests qt4-dev-tools qt4-default qt4-qtconfig qt4-qmake && \
    apt-get install -y --no-install-recommends --no-install-suggests libqt4-dev libqt4-opengl-dev libqt4-svg libqt4-network libqtwebkit-dev && \
    apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /

