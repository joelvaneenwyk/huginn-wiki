## Why run Huginn with docker

You can play with or deploy Huginn inside of [docker](http://www.docker.io/).

Getting Huginn up and running using docker is quick and painless once you have docker installed. The docker container is suitable for production and evaluation. Huginn uses environmental variables for configuration, so rather than having a .env file, the Docker container expects variables to be passed into the launch command.

## Running the Container

### Step 1: Install Docker
The website has [docker install instructions for most environments](https://docs.docker.com/installation/).

### Step 2: Launch the container

Follow the [Quick Start instructions](https://registry.hub.docker.com/u/cantino/huginn/) on the docker hub registry.

### Other options:

Other Docker options:

* https://registry.hub.docker.com/u/andrewcurioso/huginn/
* If you'd like to run Huginn's web process and job worker process in separate containers, another option is https://github.com/hackedu/huginn-docker. It also uses Unicorn as the web server and serves precompiled assets.
