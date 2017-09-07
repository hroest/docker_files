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

# /usr/lib64/qt4/bin/qmake

## this is manylinux_qt_contrib
git clone -b Release2.2.0 https://github.com/OpenMS/OpenMS.git
# git clone https://github.com/OpenMS/OpenMS.git && rm -rf OpenMS/.git/ OpenMS/share/OpenMS/examples/
RUN mkdir openms-build

WORKDIR /openms-build

for PYBIN in /opt/python/cp27*; do
echo $PYBIN
done

for PYBIN in /opt/python/cp27*; do
"$PYBIN/bin/pip" install -U Cython
"$PYBIN/bin/pip" install -U setuptools
"$PYBIN/bin/pip" install -U wheel
"$PYBIN/bin/pip" install -U numpy
"$PYBIN/bin/pip" install -U nose
"$PYBIN/bin/pip" install -U autowrap
done

export PYVER=`basename $PYBIN`
mkdir openms-build-$PYVER
cd openms-build-$PYVER

cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DPYOPENMS=On -DPYTHON_EXECUTABLE:FILEPATH=$PYBIN/bin/python -DQT_QMAKE_EXECUTABLE=/qt/bin/qmake ../OpenMS
make -j6 pyopenms


# upload stuff ... 
cd pyOpenMS
"$PYBIN/bin/pip" wheel . -w wheelhouse_tmp
for whl in wheelhouse_tmp/pyopenms*.whl; do
  auditwheel repair "$whl" -w wheelhouse/
done

# mv wheelhouse /data/





RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DPYOPENMS=On -DQT_QMAKE_EXECUTABLE=/usr/lib64/qt4/bin/qmake ../OpenMS
RUN make OpenMS

