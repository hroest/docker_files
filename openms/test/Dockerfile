FROM hroest/openms_dependencies:17.04

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && cd OpenMS && git checkout fix/map_deterministic 
# && rm -rf .git/ share/OpenMS/examples/
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DBOOST_USE_STATIC=OFF ../OpenMS

RUN make OpenMS -j6

RUN make MRMAssay_test
RUN ctest -R MRMAssay_test

RUN make -j6 


RUN apt-get -y update 
RUN apt-get -y install xvfb
RUN (Xvfb :1 -screen 0 1024x768x24 &) && export DISPLAY=:1 && ctest 

