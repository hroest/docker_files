# Concatenated script to build OpenMS
# 

# FROM hroest/openms_full:latest
FROM hroest/contrib:qt5-v2.3.1-py

ARG repo
ARG branch

RUN git clone -b $branch https://github.com/$repo.git && rm -rf OpenMS/.git/
RUN sed -i 's#2> /dev/null##' OpenMS/src/pyOpenMS/CMakeLists.txt

RUN mkdir /openms-build
WORKDIR /openms-build

# Load the Qt5 environment and configure
RUN pip install -U autowrap
RUN QT_ENV=$(find /opt -name 'qt*-env.sh') && /bin/bash -c "source ${QT_ENV} && cmake -DCMAKE_PREFIX_PATH='/contrib-build/;/usr/;/usr/local' -DBOOST_USE_STATIC=OFF -DPYOPENMS=On ../OpenMS"
RUN make -j6 pyopenms
RUN ctest -j6 -R pyopenms

