FROM hroest/openms_dependencies:v2.2.0-small

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && rm -rf OpenMS/.git/ OpenMS/share/OpenMS/examples/
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF ../OpenMS
RUN make OpenMS


