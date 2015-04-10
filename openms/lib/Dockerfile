FROM hroest/openms_dependencies 

RUN git clone https://github.com/OpenMS/OpenMS.git
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF ../OpenMS
RUN make OpenMS


