#################################################################
# Dockerfile
#
# Version:          1
# Software:         OpenMS
# Software Version: 2.0.0
# Description:      OpenS tool suite (TOPP tools only)
# Website:          http://open-ms.sourceforge.net/
# Tags:             Proteomics
# Provides:         OpenMS 2.0.0 dependencies
# Base Image:       biodckr/openms_dep:latest
# Build Cmd:        
# Pull Cmd:         
# Run Cmd:          
#################################################################

# Set the base image to OpenMS dependencies
# FROM biodckr/biod_openms_dep:latest
FROM hroest/biod_openms_dep:latest

################### BEGIN INSTALLATION ########################

WORKDIR /home/biodocker/

RUN git clone https://github.com/OpenMS/OpenMS.git

WORKDIR /home/biodocker/OpenMS/

RUN git checkout tags/Release2.0.0

WORKDIR /home/biodocker/

RUN mkdir openms-build

WORKDIR /home/biodocker/openms-build/

RUN cmake -DCMAKE_PREFIX_PATH="/home/biodocker/contrib-build/;/home/biodocker/contrib/;/usr/;/usr/local" -DBOOST_USE_STATIC=OFF -DHAS_XSERVER=Off ../OpenMS && \
  make TOPP
  #  ctest

ENV PATH /home/biodocker/openms-build/bin/:$PATH

# Change user to back to biodocker
USER biodocker

# CHANGE WORKDIR TO /DATA
WORKDIR /data/

#################### END INSTALLATION #########################

# File Author / Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>
# Modified by Felipe da Veiga Leprevost 01-26-2016

