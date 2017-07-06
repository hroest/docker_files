
# Dockerfile collection

A collection of dockerfiles to build some interesting projects such as OpenMS.
The repository contains Dockerfiles to build several releases of OpenMS as well
as nightly builds.

## OpenMS

There are Docker files available that create a container with all the
dependencies for OpenMS already pre-compiled: 

- [OpenMS dependencies](openms/dependencies/Dockerfile) 
- [OpenMS dependencies with Qt5](openms/dependencies-qt5/Dockerfile) 

## Example

Example build of a pyOpenMS container:

    cd openms/releases/2.2/py
    sudo docker build .
    sudo docker tag 96f09cf61605 hroest/openms-pyopenms-v2.2.0
    sudo docker push hroest/openms-pyopenms-v2.2.0


