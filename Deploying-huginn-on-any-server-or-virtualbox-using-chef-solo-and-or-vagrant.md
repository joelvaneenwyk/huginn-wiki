_This documentation is not yet complete.  The Vagrant and Chef setup for Huginn has not been merged into master yet._

[Chef](http://www.opscode.com/chef/) cookbooks for deploying Huginn are available in `deployment`. Use the role `role[huginn_production]` to deploy Huginn to a _production_ environment or the role `role[huginn_development]` to deploy to a _development_ environment.

Here are instructions for deploying Huginn to any server using [chef solo](http://docs.opscode.com/chef_solo.html).

First, install [knife-solo](http://matschaffer.github.io/knife-solo/):

    gem install knife-solo
 
This will also install chef solo.

Next, install the [librarian-chef](https://github.com/applicationsonline/librarian-chef) gem:

    gem install librarian-chef

Install the cookbooks listed in the Cheffile by running:

    cd deployment && librarian-chef install

Now, to deploy Huginn in _production_ mode on any server, run:

    knife solo bootstrap [user@]hostname -r role[huginn_production]

You can provide ssh options like `-i` (identity file) and `-p` (SSH port) to knife if needed. When this finishes, Huginn should be installed and running on your server at port 80. Visit your server to check it out. A new user has been created for managing Huginn with username `huginn` and password `huginn` (please change it right away by logging in and typing `passwd`). Huginn is installed in the home directory of `huginn` at `/home/huginn`. Setup follows [Capistrano](https://github.com/capistrano/capistrano) standards, so the `current`, `shared`, and `releases` directories are present with `current` symlinked to the most recent deployment in `releases`. Nginx is running and proxy-passing to a [Unicorn](http://unicorn.bogomips.org/) server, with config files at `/etc/nginx/nginx.conf` and `/home/huginn/shared/config/unicorn.rb` respectively, which you can change according to your needs and redeploy by running above mentioned command. Before reploying, make sure that Huginn isn't already running by stopping it with `sudo stop huginn`. You can start, stop, or restart Huginn with these commands:

    sudo start huginn
    sudo stop huginn
    sudo restart huginn

You can also use [Vagrant](http://www.vagrantup.com/) to play with Huginn locally or even to spin up an EC2 server. First, install the following Vagrant plugins:

    vagrant plugin install vagrant-aws
    vagrant plugin install vagrant-omnibus

To install Huginn on an EC2 instance, fill out `aws.access_key_id`, `aws.secret_access_key`, `aws.keypair_name`, and `override.ssh.private_key_path` in the Vagrantfile and run

    vagrant up ec2 --provider=aws

It'll install Huginn on a newly created EC2 instance in Rails's _production_ environment mode. It uses the same chef role `role[huginn_production]` as mentioned above.

You can ssh into your new EC2 instance or destroy it:

    vagrant ssh ec2
    vagrant destroy ec2

You can also play with Huginn in a local [VirtualBox](https://www.virtualbox.org/) virtual machine running on your computer:

    vagrant up vb

This tells Vagrant to launch a VirtualBox virtual machine and install Huginn on it. You should now be able to visit `http://localhost:3000` to use Huginn on your local computer. It uses the `role[huginn_development]` chef role.  A new user with username `huginn` and password `huginn` is created and Huginn is installed at `/home/huginn/huginn`

You can ssh into the virtual machine or destroy it:

    vagrant ssh vb
    vagrant destroy vb