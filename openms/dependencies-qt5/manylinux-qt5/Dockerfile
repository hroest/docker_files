FROM quay.io/pypa/manylinux1_x86_64

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
RUN wget http://download.qt.io/official_releases/qt/5.9/5.9.4/single/qt-everywhere-opensource-src-5.9.4.tar.xz && \
    xz -d qt-everywhere*src-5.*.tar.xz && \
    tar xf qt-everywhere*src-5.*.tar && \
    cd /qt-everywhere*src-5.* && \
    sed -i "s/#define QTESTLIB_USE_PERF_EVENTS/#undef QTESTLIB_USE_PERF_EVENTS/g" qtbase/src/testlib/qbenchmark_p.h && \
    ./configure -openssl -opensource -nomake examples -nomake tests -opengl desktop -confirm-license -prefix /qt \
      -D _X_INLINE=inline -D XK_dead_currency=0xfe6f -D XK_ISO_Level5_Lock=0xfe13 -D FC_WEIGHT_EXTRABLACK=215 -D FC_WEIGHT_ULTRABLACK=FC_WEIGHT_EXTRABLACK -D GLX_GLXEXT_PROTOTYPES=On \
      -skip activeqt -skip androidextras -skip connectivity -skip enginio -skip location -skip macextras -skip multimedia -skip sensors -skip serialport \
      -skip wayland -skip webchannel -skip websockets -skip winextras -skip x11extras -skip qtgamepad && \
    make && \
    make install && \
    cd / && \
    rm -rf qt-everywhere*src-5.*

## this is hroest/manylinux_qt59:v3

RUN yum install -y libtool
RUN yum install -y libzip-devel zlib-devel bzip2-devel

RUN wget http://cmake.org/files/v3.10/cmake-3.10.0.tar.gz && \
    tar xzvf cmake-3.10.0.tar.gz && \
    cd /cmake-3.10.0 && \
    ./bootstrap && \
    make && \
    make install && \
    cd / && \
    rm -rf /cmake-*


# install contrib
RUN git clone https://github.com/OpenMS/contrib.git && \
    cd contrib && git checkout 0022e80d2ce7660a795a7131a56ed3 && cd .. && \
    mkdir contrib-build && \
    cd /contrib-build && \
    cmake -DBUILD_TYPE=ALL ../contrib && \
    rm -rf archives src && \
    cd / && \
    rm -rf contrib

WORKDIR /

## this is hroest/manylinux_qt59_contrib:v4.1

# -------------------------------------------
# manually install cmake3.10 && compile HDF5:
# -> this is hroest/manylinux_qt59_contrib:v3.2

