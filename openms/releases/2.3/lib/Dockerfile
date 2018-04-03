FROM hroest/openms_dependencies 

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd /OpenMS && git checkout tags/Release2.3.0 && rm -rf .git

RUN mkdir openms-build
WORKDIR /openms-build

## only b/c screwed up cmake ...
RUN sudo apt-get remove -y cmake cmake-data && sudo -E apt-get update && sudo apt-get -y install cmake

RUN /usr/bin/cmake -DCMAKE_PREFIX_PATH="/usr/;/usr/local" -DOPENMS_CONTRIB_LIBS="/contrib-build/"  -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off ../OpenMS

# make OpenMS library
RUN make OpenMS -j6

