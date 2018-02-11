FROM quay.io/pypa/manylinux1_x86_64

RUN wget --no-check-certificate http://cmake.org/files/v3.9/cmake-3.9.0.tar.gz
RUN tar xzvf cmake-3.9.0.tar.gz 
WORKDIR /cmake-3.9.0
RUN ./bootstrap
RUN make 
RUN make install
WORKDIR /

# ##### See instructions at https://kate-editor.org/2014/12/22/qt-5-4-on-red-hat-enterprise-5/
# ##### patch qbenchmark: no perf events => patch that out, won't compile, at least not for me because of missing syscall/broken kernel header
# ##### configure with some defines to work on centos 5 (fake some defines)
# ##### qtgamepad has some issues with undefined BTN_TRIGGER_HAPPY, either remove it or try the solution at http://lists.qt-project.org/pipermail/development/2017-March/029188.html 
RUN yum install -y xz     
RUN wget http://download.qt.io/official_releases/qt/5.9/5.9.4/single/qt-everywhere-opensource-src-5.9.4.tar.xz && \
    xz -d qt-everywhere-opensource-src-5.9.4.tar.xz  && \
    tar xvf qt-everywhere-opensource-src-5.9.4.tar && \
    cd /qt-everywhere-opensource-src-5.9.4 && \
    sed -i "s/#define QTESTLIB_USE_PERF_EVENTS/#undef QTESTLIB_USE_PERF_EVENTS/g" qtbase/src/testlib/qbenchmark_p.h && \
    ./configure -opensource -nomake examples -nomake tests -opengl desktop -confirm-license -prefix /qt \
      -D _X_INLINE=inline -D XK_dead_currency=0xfe6f -D XK_ISO_Level5_Lock=0xfe13 -D FC_WEIGHT_EXTRABLACK=215 -D FC_WEIGHT_ULTRABLACK=FC_WEIGHT_EXTRABLACK -D GLX_GLXEXT_PROTOTYPES=On \
      -skip activeqt -skip androidextras -skip connectivity -skip enginio -skip location -skip macextras -skip multimedia -skip quick1 -skip sensors -skip serialport \
      -skip wayland -skip webchannel -skip websockets -skip winextras -skip x11extras -skip qtgamepad && \
    make && \
    make install && \
    cd / && \
    rm -rf qt-everywhere-opensource-src*

## this is hroest/manylinux_qt59

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

# small bugfix
RUN ln -s /contrib-build/lib64/libxerces-c-3.2.a /contrib-build/lib64/libxerces-c.a

## this is hroest/manylinux_qt59_contrib

