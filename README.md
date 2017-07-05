
# Dockerfile collection

A collection of dockerfiles to build some interesting projects such as OpenMS.
The repository contains Dockerfiles to build several releases of OpenMS as well
as nightly builds.

## Example

Example build of a pyOpenMS container:

    cd openms/releases/2.2/py
    sudo docker build .
    sudo docker tag 96f09cf61605 hroest/openms-pyopenms-v2.2.0
    sudo docker push hroest/openms-pyopenms-v2.2.0


