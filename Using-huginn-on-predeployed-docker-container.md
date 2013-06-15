
You can play with Huginn inside of [docker](http://www.docker.io/).  Start by checking out the docker repository.

*Step 1* This step is only needed if you can't run docker natively (on a Mac, for example), and so are going to run docker inside of Vagrant.  Add `config.vm.forward_port 3000, 3000` to the Vagrant file in the docker repository, then run `vagrant up`.

*Step 2* Run:

    docker pull rishabh/huginn
    docker run -h localhost -d -p 3000 rishabh/huginn /bin/bash -c "su huginn -c runhuginn"

This will output id of newly created container. To get local ip address of container, run:

    docker inspect <containerId>

And get ip address from there, Now huginn is running at `<localipaddress:3000>`, Port 3000 of this container is mapped with a host port, which you can see by:

    docker port <containerId> 3000

Now, you can play with huginn at `<hostipaddress>:<portnumber>` which is same as `<localipaddress:3000>`. A new user with username `huginn` and password `huginn` is created for management of huginn.