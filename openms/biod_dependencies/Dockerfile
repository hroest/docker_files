#################################################################
# Dockerfile
#
# Version:          1
# Software:         OpenMS
# Software Version: 2.0.0
# Description:      OpenS tool suite (dependencies only)
# Website:          http://open-ms.sourceforge.net/
# Tags:             Proteomics
# Provides:         OpenMS 2.0.0 dependencies
# Base Image:       biodckr/biodocker:latest
# Build Cmd:        
# Pull Cmd:         
# Run Cmd:          
#################################################################

# Set the base image to Ubuntu
FROM biodckr/biodocker:latest

################### BEGIN INSTALLATION ########################

# Change user to root
USER root

# Installing dependencies
RUN apt-get -y update && \
    apt-get install -y \
    cmake \
    g++ \
    autoconf \
    qt4-dev-tools \
    patch \
    libtool \
    make \
    git \
    software-properties-common \
    python-software-properties \
    libboost-all-dev \
    libsvm-dev \
    libglpk-dev \
    libzip-dev \
    zlib1g-dev \
    libxerces-c-dev \
    libbz2-dev && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Get contrib & setting folders
WORKDIR /home/biodocker/

RUN git clone https://github.com/OpenMS/contrib.git && \
    mkdir /home/biodocker/contrib-build/

# Change wordir to start building
WORKDIR /home/biodocker/contrib-build/

RUN cmake -DBUILD_TYPE=SEQAN ../contrib && \
    cmake -DBUILD_TYPE=WILDMAGIC ../contrib && \
    cmake -DBUILD_TYPE=EIGEN ../contrib

