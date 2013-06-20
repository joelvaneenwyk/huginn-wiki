You can play with Huginn inside of [docker](http://www.docker.io/).  Start by checking out the docker repository.

*Step 1*: This step is only needed if you can't run docker natively (on a Mac, for example), and so are going to run docker inside of Vagrant.  Huginn needs a fair amount of RAM, so in the docker Vagrantfile, update `config.vm.provider :virtualbox do |vb|` like so:

    config.vm.provider :virtualbox do |vb|
      config.vm.box = BOX_NAME
      config.vm.box_url = BOX_URI
      vb.customize ["modifyvm", :id, "--memory", "1800"]
    end
    config.vm.forward_port 80, 3000

Now you can run `vagrant up`.

*Step 2*:

 * Run:

        docker pull rishabh/huginn
        docker run -h localhost -d -p 3000:80 rishabh/huginn /bin/bash -c "su huginn -c runhuginn"

  This starts a Huginn process in a docker container with a new internal user to manage it (`huginn`/`huginn`).

 * Run `docker ps` to see the now-running Huginn container. Port 3000 of docker container is mapped with port 80 on your computer (or your VirtualBox machine if you did _Step 1_).  You can also run `docker inspect <containerId>` for more details.

 * If docker is running natively on your computer, you can now connect to the host port to use Huginn.  If you're using Vagrant, Host port 80 has been forwarded to port 3000 of your computer. Now you should be able to connect to localhost:3000 on your computer and play with Huginn.