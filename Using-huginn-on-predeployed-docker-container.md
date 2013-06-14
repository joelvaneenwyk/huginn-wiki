To play with huginn on [docker](http://www.docker.io/), run:

    docker pull rishabh/huginn
    docker run -h localhost -d -p 3000 rishabh/huginn /bin/bash -c "su huginn -c runhuginn"

This will output id of newly created container. To get local ip address of container, run:

    docker inspect <containerId>

And get ip address from there, Now huginn is running at `<localipaddress:3000>`, Port 3000 of this container is mapped with a host port, which you can see by:

    docker port <containerId> 3000

Now, you can play with huginn at `<hostipaddress>:<portnumber>` which is same as `<localipaddress:3000>`. A new user with username `huginn` and password `huginn` is created for management of huginn.