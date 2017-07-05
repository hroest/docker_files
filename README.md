
Dockerfile collection

=== Example ===

Example build of a pyOpenMS container:

    cd openms/releases/2.2/py
    sudo docker build .
    sudo docker tag 96f09cf61605 hroest/openms-pyopenms-v2.2.0
    sudo docker push hroest/openms-pyopenms-v2.2.0


