FROM hroest/openms_dependencies:v2.2.0-small

WORKDIR /
RUN git clone https://github.com/OpenMS/OpenMS.git && \
  hash=`git log | head -n 1 | cut -f 2 -d ' '` && \
  sed -i "s/OPENMS_GIT_SHA1/$hash/" source/CONCEPT/VersionInfo.cpp && \
  rm -rf OpenMS/.git/ OpenMS/share/OpenMS/examples/
RUN mkdir openms-build

WORKDIR /openms-build

RUN cmake -DCMAKE_PREFIX_PATH="/contrib-build/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF ../OpenMS
RUN make OpenMS


