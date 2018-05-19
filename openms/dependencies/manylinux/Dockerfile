FROM quay.io/pypa/manylinux1_x86_64

RUN wget --no-check-certificate http://cmake.org/files/v3.9/cmake-3.9.0.tar.gz
RUN tar xzvf cmake-3.9.0.tar.gz 
WORKDIR /cmake-3.9.0
RUN ./bootstrap
RUN make 
RUN make install
WORKDIR /

# install qt
RUN wget http://download.qt.io/official_releases/qt/4.8/4.8.7/qt-everywhere-opensource-src-4.8.7.tar.gz && \
    tar xzvf qt-everywhere-opensource-src-4.8.7.tar.gz && \
    cd /qt-everywhere-opensource-src-4.8.7 && \
    ./configure -opensource -nomake demos -nomake examples -no-script -webkit -confirm-license  -prefix /qt && \
    make &&  \
    make install && \
    cd / && \
    rm -rf qt-everywhere-opensource-src-4.8.7*

## this is manylinux_qt
RUN yum install -y libtool
RUN yum install -y libzip-devel zlib-devel bzip2-devel


# install contrib
RUN git clone https://github.com/OpenMS/contrib.git && \
    mkdir contrib-build && \
    cd /contrib-build && \
    cmake -DBUILD_TYPE=ALL ../contrib && \
    rm -rf archives src \
    cd / && \
    rm -rf contrib

WORKDIR /

## this is manylinux_qt_contrib

# OpenSSL 1.1 is too modern...
RUN wget https://www.openssl.org/source/openssl-1.0.2n.tar.gz && \
    tar xzvf openssl-*.tar.gz  && \
    cd openssl-* && \
    ./config -fpic shared --prefix=/usr --openssldir=/usr && make && make install && \
    rm -rf /openssl*

RUN wget http://files.directadmin.com/services/wget-1.8.2.tar.gz && \
  tar xvzf wget-1.8.2.tar.gz && \
  cd wget-1.8.2 && \
  ./configure --prefix=/usr --with-ssl && \
  make && \
  make install && \
  rm -rf /wget*

## this is manylinux_qt_contrib:v2

