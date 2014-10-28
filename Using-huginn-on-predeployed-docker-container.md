## Why run Huginn with docker

You can play with or deploy Huginn inside of [docker](http://www.docker.io/).

Getting Huginn up and running using docker is quick and painless once you have docker installed. The docker container is suitable for production and evaluation. Huginn uses environmental variables for configuration, so rather than having a .env file, the Docker container expects variables to be passed into the launch command.

The below instructions work well, but if you'd like to run Huginn's web process and job worker process in separate containers, check out https://github.com/hackedu/huginn-docker. It also uses Unicorn as the web server and serves precompiled assets.

## Running the Container

### Step 1: Install Docker
The website has [docker install instructions for most environments](https://docs.docker.com/installation/).  If you already have Docker installed, you'll need to upgrade to something recentish - 0.10.0 was too old, but 1.1.2 worked fine.

### Step 2: Launch the container

Follow the [Quick Start instructions](https://registry.hub.docker.com/u/andrewcurioso/huginn/) on the docker hub registry.

### Step 3: Launch Huginn

Open up a web browser to Huginn. If you followed the instructions exactly, by default it listens on port 3000. So you can type in `localhost:3000` in your browser to go to Huginn.

If you are using boot2docker (for OSX) you will want to use the IP of the boot2docker virtual machine. By default the address would be `192.168.59.103:3000`. If that doesn't work you can get the current IP of the virtual machine using `boot2docker ip` in the command line.