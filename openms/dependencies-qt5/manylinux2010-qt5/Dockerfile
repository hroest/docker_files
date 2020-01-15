FROM quay.io/pypa/manylinux2010_x86_64

# OpenSSL 1.1 is too modern...
RUN curl -L -o openssl-1.tar.gz https://www.openssl.org/source/openssl-1.0.2n.tar.gz && \
    tar xzvf openssl-*.tar.gz  && \
    cd openssl-* && \
    ./config -fpic shared --prefix=/usr --openssldir=/usr && make && make install && \
    rm -rf /openssl*

RUN curl -L -o wget-1.8.2.tar.gz http://files.directadmin.com/services/wget-1.8.2.tar.gz && \
  tar xvzf wget-1.8.2.tar.gz && \
  cd wget-1.8.2 && \
  ./configure --prefix=/usr --with-ssl && \
  make && \
  make install && \
  rm -rf /wget*

# ##### See instructions at https://kate-editor.org/2014/12/22/qt-5-4-on-red-hat-enterprise-5/
# ##### patch qbenchmark: no perf events => patch that out, won't compile, at least not for me because of missing syscall/broken kernel header
# ##### configure with some defines to work on centos 5 (fake some defines)
# ##### qtgamepad has some issues with undefined BTN_TRIGGER_HAPPY, either remove it or try the solution at http://lists.qt-project.org/pipermail/development/2017-March/029188.html 
RUN yum install -y xz 
# RUN wget http://download.qt.io/official_releases/qt/5.11/5.11.2/single/qt-everywhere-src-5.11.2.tar.xz && \
# RUN wget http://download.qt.io/official_releases/qt/5.10/5.10.1/single/qt-everywhere-src-5.10.1.tar.xz && \
# RUN wget http://download.qt.io/official_releases/qt/5.9/5.9.4/single/qt-everywhere-opensource-src-5.9.4.tar.xz && \ # will work
# RUN wget http://download.qt.io/official_releases/qt/5.6/5.6.3/single/qt-everywhere-opensource-src-5.6.3.tar.xz && \ # will not work b/c signalfd.h
# -skip quick1 -skip qtgamepad # only in 5.9
# -skip quick1 # drop for 5.11 
RUN wget http://download.qt.io/official_releases/qt/5.9/5.9.4/single/qt-everywhere-opensource-src-5.9.4.tar.xz && \
    xz -d qt-everywhere*src-5.*.tar.xz && \
    tar xf qt-everywhere*src-5.*.tar && \
    cd /qt-everywhere*src-5.* && \
    sed -i "s/#define QTESTLIB_USE_PERF_EVENTS/#undef QTESTLIB_USE_PERF_EVENTS/g" qtbase/src/testlib/qbenchmark_p.h && \
    ./configure -openssl -opensource -nomake examples -nomake tests -opengl desktop -confirm-license -prefix /qt \
      -D _X_INLINE=inline -D XK_dead_currency=0xfe6f -D XK_ISO_Level5_Lock=0xfe13 -D FC_WEIGHT_EXTRABLACK=215 -D FC_WEIGHT_ULTRABLACK=FC_WEIGHT_EXTRABLACK -D GLX_GLXEXT_PROTOTYPES=On -skip qtgamepad -skip quick1 && \
    make && \
    make install && \
    cd / && \
    rm -rf qt-everywhere*src-5.*

RUN wget http://cmake.org/files/v3.14/cmake-3.14.0.tar.gz && \
    tar xzvf cmake-3.14.0.tar.gz && \
    cd /cmake-3.14.0 && \
    ./bootstrap && \
    make && \
    make install && \
    cd / && \
    rm -rf /cmake-*

RUN yum install -y libtool
RUN yum install -y libzip-devel zlib-devel bzip2-devel

# install contrib
RUN git clone https://github.com/OpenMS/contrib.git && \
    mkdir contrib-build && \
    cd /contrib-build && \
    cmake -DBUILD_TYPE=ALL ../contrib && \
    rm -rf archives src && \
    cd / && \
    rm -rf contrib

WORKDIR /

# Metadata
LABEL base.image="manylinux2010_x86_64"
LABEL version="2.0"
LABEL software="OpenMS (dependencies for manylinux2010)"
LABEL software.version="qt5-v2.5.1"
LABEL description="C++ libraries and tools for MS/MS data analysis"
LABEL website="http://www.openms.org/"
LABEL documentation="http://www.openms.org/"
LABEL license="http://www.openms.org/"
LABEL tags="Proteomics"

