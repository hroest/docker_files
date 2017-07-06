
# Dockerfile collection

A collection of dockerfiles to build some interesting projects such as OpenMS.
The repository contains Dockerfiles to build several releases of OpenMS as well
as nightly builds.

## OpenMS

There are Docker files available that create a container with all the
dependencies for OpenMS already pre-compiled: 

- [OpenMS dependencies](openms/dependencies/Dockerfile) 
- [OpenMS dependencies with Qt5](openms/dependencies-qt5/Dockerfile) 

Based on these containers, it is pretty straight forward to build the

- (i) [OpenMS library](openms/lib/Dockerfile) 
- (ii) [OpenMS executables](openms/executables/Dockerfile) 


Using the same base container, we also have Docker files for the releases

- [OpenMS release 2.0](openms/releases/2.0) 
- [OpenMS release 2.1](openms/releases/2.1) 
- [OpenMS release 2.2](openms/releases/2.2) 
- [OpenMS branch qt5](openms/releases/qt5) 

## Example

Example build of a pyOpenMS container:

    cd openms/releases/2.2/py
    sudo docker build .
    sudo docker tag 96f09cf61605 hroest/openms-pyopenms-v2.2.0
    sudo docker push hroest/openms-pyopenms-v2.2.0


