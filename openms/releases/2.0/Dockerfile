FROM hroest/openms_dependencies 

# # # Checkout OpenMS 2.0
# for git > 1.8x this should work
# RUN git clone --branch tags/Release2.0.0 https://github.com/OpenMS/OpenMS.git
# however we use the more backward compatible version:

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git
WORKDIR /OpenMS
RUN git checkout tags/Release2.0.0
WORKDIR /

RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off ../OpenMS

# make all of OpenMS
RUN make 
RUN ctest


