# Concatenated script to build OpenMS
# 

# FROM hroest/openms_full:latest
FROM hroest/contrib:qt5-v2.5.0

RUN apt-get update -y && apt-get install -y python-pip python-dev python-numpy
RUN pip install nose
RUN pip install -U setuptools
RUN pip install autowrap==0.19.0
RUN pip install -U Cython==0.25

ARG repo
ARG branch

RUN echo $repo
RUN echo $branch
RUN git clone -b $branch https://github.com/$repo.git && rm -rf OpenMS/.git/
RUN sed -i 's#2> /dev/null##' OpenMS/src/pyOpenMS/CMakeLists.txt

RUN mkdir /openms-build
WORKDIR /openms-build

# Load the Qt5 environment and configure
RUN QT_ENV=$(find /opt -name 'qt*-env.sh') && /bin/bash -c "source ${QT_ENV} && cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF -DPYOPENMS=On ../OpenMS"
RUN make -j6 OpenMS
RUN make -j6 pyopenms
RUN ctest -j6 -R pyopenms

