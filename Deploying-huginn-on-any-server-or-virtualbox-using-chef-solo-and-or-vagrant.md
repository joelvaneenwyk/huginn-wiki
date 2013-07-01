_This documentation is not yet complete.  The Vagrant and Chef setup for Huginn has not been merged into master yet._

[EC2 with Chef](#chef-ec2)

[Vagrant (EC2)](#ec2-vagrant)

[Vagrant (locally)](#local-vagrant)

# <a name="chef-ec2"/>Deploying Huginn to EC2 with Chef

[Chef](http://www.opscode.com/chef/) cookbooks for deploying Huginn are available in `deployment`. Use the role `role[huginn_production]` to deploy Huginn to a _production_ environment or the role `role[huginn_development]` to deploy to a _development_ environment.

Here are instructions for deploying Huginn to any server using [chef solo](http://docs.opscode.com/chef_solo.html).

First, install [knife-solo](http://matschaffer.github.io/knife-solo/):

    gem install knife-solo
 
This will also install chef solo.

Next, install the [librarian-chef](https://github.com/applicationsonline/librarian-chef) gem:

    gem install librarian-chef

Install the cookbooks listed in the Cheffile by running:

    cd deployment && librarian-chef install

Now, to deploy Huginn in _production_ mode on a newly created EC2 instance, run:

    knife solo bootstrap [user@]hostname -r role[huginn_production]

You can provide ssh options like `-i` (identity file) and `-p` (SSH port) to knife if needed. When this finishes, Huginn should be installed and running on your server at port 80. Visit your server to check it out. A new user has been created for managing Huginn with username `huginn` and password `huginn` (please change it right away by logging in and typing `passwd`). Huginn is installed in the home directory of `huginn` at `/home/huginn`. Setup follows [Capistrano](https://github.com/capistrano/capistrano) standards, so the `current`, `shared`, and `releases` directories are present with `current` symlinked to the most recent deployment in `releases`. Nginx is running and proxy-passing to a [Unicorn](http://unicorn.bogomips.org/) server, with config files at `/home/huginn/shared/config/nginx.conf` and `/home/huginn/shared/config/unicorn.rb` respectively, which you can change according to your needs and redeploy by running above mentioned command. Before redeploying, make sure that Huginn isn't already running by stopping it with `sudo stop huginn`. You can start, stop, or restart Huginn with these commands:

    sudo start huginn
To install Huginn on an EC2 instance, fill out `aws.access_key_id`, `aws.secret_access_key`, `aws.keypair_name`, and `override.ssh.private_key_path` in the `deployment/Vagrantfile` and run
    sudo stop huginn
    sudo restart huginn

If you would like to use your private Huginn repo, then you will have to replace `https://github.com/cantino/huginn` with the URL of your Huginn private repo in the `deploy` resource's `repo` attribute here: `deployment/site-cookbooks/huginn_production/recipes/default.rb`.

# Deploying Huginn with Vagrant

You can also use [Vagrant](http://www.vagrantup.com/) to play with Huginn locally or even to spin up an EC2 server for experimentation. 

## <a name="ec2-vagrant"/>EC2 Vagrant 

It'll install Huginn on a newly created EC2 instance in Rails's _production_ environment mode. It uses the same chef role `role[huginn_production]` as mentioned above.

###### Install necessary plugins
    vagrant plugin install vagrant-aws
    vagrant plugin install vagrant-omnibus
###### Download Huginn
    git clone git://github.com/cantino/huginn.git
    cd huginn/deployment
###### Set AWS variables
Fill out `aws.access_key_id`, `aws.secret_access_key`, `aws.keypair_name`, and `override.ssh.private_key_path` in `deployment/Vagrantfile`
###### Start the instance using the Virtualbox provider
    vagrant up ec2 --provider=aws
###### Connect to the EC2 instance with SSH
    vagrant ssh ec2
###### Disconnect from the instance
    exit
###### Stop and destroy the EC2 instance
    vagrant destroy ec2

## <a name="local-vagrant"/>Local Vagrant 
###### Install necessary plugins
    vagrant plugin install vagrant-omnibus
###### Download Huginn
    git clone git://github.com/cantino/huginn.git
###### Start the VM using the Virtualbox provider
    cd huginn/deployment
    vagrant up vb
###### Connect to the VM with SSH
    vagrant ssh

You should now be able to visit `http://localhost:3000` to use Huginn on your local computer. It uses the `role[huginn_development]` chef role.  A new user with username `huginn` and password `huginn` is created and Huginn is installed at `/home/huginn/huginn`

#### <a name="other-vagrant"/>Other vagrant commands worth knowing
###### Disconnect from the VM
    exit
###### Stop the VM gracefully
    vagrant halt
###### Stop the VM forcefully (like unplugging the power from a machine)
    vagrant halt -f
###### Stop and destroy the VM (and anything you change while using it)
    vagrant destroy