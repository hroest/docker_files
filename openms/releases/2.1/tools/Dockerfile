
FROM hroest/openms-lib-v2.1.0

WORKDIR /openms-build

# make OpenMS all
RUN make TOPP -j6
RUN make UTILS -j6
RUN make -j6
RUN ctest 

