## use local copy of docker lib
FROM hroest/openms-lib-v2.1.0

WORKDIR /openms-build

RUN apt-get install -y python-pip
RUN apt-get install -y python-dev python-numpy
RUN pip install nose
RUN pip install -U setuptools
RUN pip install autowrap==0.8.0
RUN pip install Cython==0.23.0
RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DPYOPENMS=On ../OpenMS

# make OpenMS library
RUN make pyopenms


