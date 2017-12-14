FROM ubuntu:12.04

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

RUN apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ autoconf patch libtool make git && \
         apt-get install -y --no-install-recommends --no-install-suggests software-properties-common python-software-properties && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# forgot automake ! 
RUN apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests g++ automake && \
         apt-get install -y --no-install-recommends --no-install-suggests cmake && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# forgot automake ! 
RUN apt-get -y update && \
         apt-get install -y --no-install-recommends --no-install-suggests wget && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# RUN wget https://github.com/OpenMS/OpenMS/archive/Release1.11.1.tar.gz
RUN wget -O Release.1.11.1.tar.gz 'https://downloads.sourceforge.net/project/open-ms/OpenMS/OpenMS-1.11.1/OpenMS-1.11.1.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fopen-ms%2Ffiles%2FOpenMS%2FOpenMS-1.11.1%2F&ts=1513224931&use_mirror=cytranet'
RUN tar xzvf Release.1.11.1.tar.gz

## #RUN git clone https://github.com/OpenMS/contrib.git && cd contrib && git checkout 94f701dbcdc7b7205ad40bd6b301c17ffce35e6c && rm -rf contrib/.git/
## RUN git clone https://github.com/OpenMS/contrib.git && cd contrib && git checkout 00e2759b4c7266fce1ef8fa47bf303f19df6b59b && rm -rf contrib/.git/
## RUN mkdir contrib-build

WORKDIR /contrib-build
RUN cmake -DBUILD_TYPE=ALL ../OpenMS-1.11.1/contrib/ && rm -rf archives src

# install dependencies
RUN apt-get -y update 

RUN apt-get install -y cmake 
RUN apt-get install -y --no-install-recommends --no-install-suggests qt4-dev-tools qt4-qtconfig qt4-qmake && \
         apt-get install -y --no-install-recommends --no-install-suggests libqt4-dev libqt4-opengl-dev libqt4-svg && \
         apt-get install -y --no-install-recommends --no-install-suggests libqt4-webkit libqtwebkit-dev && \
         apt-get clean && \
         apt-get purge && \
         rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd /OpenMS && git checkout tags/Release1.9 && rm -rf .git

RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_FIND_ROOT_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off ../OpenMS

# make OpenMS library
RUN make OpenMS -j6
RUN make TOPP
RUN make UTILS

ENV PATH /openms-build/bin/:$PATH
ENV LD_LIBRARY_PATH /openms-build/lib/:$LD_LIBRARY_PATH


