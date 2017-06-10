FROM hroest/openms_dependencies 

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git
WORKDIR /OpenMS
RUN git checkout tags/Release2.1.0
WORKDIR /

RUN mkdir openms-build

WORKDIR /openms-build

## only b/c screwed up cmake ...
RUN sudo apt-get remove -y cmake cmake-data
# sudo -E add-apt-repository -y ppa:george-edison55/cmake-3.x
RUN sudo -E apt-get update
RUN sudo apt-get -y install cmake

RUN which cmake 
RUN /usr/bin/cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off ../OpenMS

# make OpenMS library
RUN make OpenMS -j6


