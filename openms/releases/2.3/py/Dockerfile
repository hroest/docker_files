FROM hroest/openms-lib-2.3

WORKDIR /openms-build

RUN apt-get install -y python-pip python-dev python-numpy
RUN pip install nose
RUN pip install -U setuptools
RUN pip install Cython==0.25.2
RUN pip install autowrap==0.13.1
RUN cmake -DCMAKE_PREFIX_PATH="/usr/;/usr/local" -DOPENMS_CONTRIB_LIBS="/contrib-build/" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off -DPYOPENMS=On ../OpenMS

# make OpenMS library
RUN make pyopenms

# install
WORKDIR /openms-build/pyOpenMS
RUN python setup.py install
WORKDIR /
ENV PATH="/openms-build/bin/:${PATH}"

