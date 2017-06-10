## use local copy of docker lib
FROM hroest/openms-lib-v2.1.0

WORKDIR /openms-build

RUN apt-get install -y python-pip
RUN apt-get install -y python-dev python-numpy cython
RUN pip install autowrap
RUN pip install nose
RUN pip install -U setuptools
RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DPYOPENMS=On ../OpenMS

# make OpenMS library
RUN make pyopenms


