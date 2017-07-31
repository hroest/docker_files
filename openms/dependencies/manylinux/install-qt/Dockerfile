FROM hroest/manylinux-openms-dep

RUN wget http://download.qt.io/official_releases/qt/4.8/4.8.7/qt-everywhere-opensource-src-4.8.7.tar.gz
RUN tar xzvf qt-everywhere-opensource-src-4.8.7.tar.gz

WORKDIR /qt-everywhere-opensource-src-4.8.7

RUN ./configure -opensource -nomake demos -nomake examples -no-script -webkit -confirm-license  -prefix /qt
RUN make
RUN make install

WORKDIR /
