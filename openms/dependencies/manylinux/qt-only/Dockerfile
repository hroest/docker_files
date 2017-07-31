FROM quay.io/pypa/manylinux1_x86_64

# install qt
RUN wget http://download.qt.io/official_releases/qt/4.8/4.8.7/qt-everywhere-opensource-src-4.8.7.tar.gz && \
    tar xzvf qt-everywhere-opensource-src-4.8.7.tar.gz && \
    cd /qt-everywhere-opensource-src-4.8.7 && \
    ./configure -opensource -nomake demos -nomake examples -no-script -webkit -confirm-license  -prefix /qt && \
    make &&  \
    make install && \
    cd / && \
    rm -rf qt-everywhere-opensource-src-4.8.7*

