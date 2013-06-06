_This documentation is not yet complete.  The Vagrant and Chef setup for Huginn has not been merged into master yet._

[Chef](http://www.opscode.com/chef/) cookbooks for deploying Huginn are available in `deployment`. Use the role `role[huginn_production]` to deploy Huginn to a production environment or the role `role[huginn_development]` to deploy to a development environment.

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

Other ssh option like `-i, -p, -P` can also be used. Now, huginn has been installed and is running on your server at port 80. Visit your server to check it out. A new user has been created for managing huginn with username `huginn` and password `huginn`. Huginn is installed at home directory of user `huginn` at `/home/huginn`. Setup follows capistrano structure, so `current`, `shared`, and `releases` directories are present. Nginx and [Unicorn]() servers are used, with their config files at `/etc/nginx/nginx.conf` and `~/shared/config/unicorn.rb` respectively, which you can change according to your needs and redeploy by running above mentioned command. Before reploying, make sure, huginn already isn't running, you can stop it by `sudo stop huginn`. You can start, stop or restart huginn by

    sudo start huginn
    sudo stop huginn
    sudo restart huginn

You can also use [Vagrant](http://www.vagrantup.com/) to deploy huginn. First install following vagrant plugins by running

    vagrant plugin install vagrant-aws
    vagrant plugin install vagrant-omnibus

To install huginn on ec2 instance, fill `aws.access_key_id`, `aws.secret_access_key`, `aws.keypair_name` and `override.ssh.private_key_path` in the Vagrantfile and run

    vagrant up ec2 --provider=aws

It'll install huginn on a newly created ec2 instance in production environment. It uses same chef role `huginn_production` as mentioned above.

You can ssh into ec2 instance or destroy it by

    vagrant ssh ec2
    vagrant destroy ec2

To install Huginn on a [VirtualBox](https://www.virtualbox.org/) virtual machine:

    vagrant up vb

The second case tells Vagrant to launch a VirtualBox virtual machine and install Huginn on it. You should now be able to visit `http://localhost:3000` to use Huginn on your local computer. It uses `huginn_development` chef role. A new user with username `huginn` and password `huginn` is created and huginn is installed at `/home/huginn/huginn`

You can ssh into virtual machine or destroy it by:

    vagrant ssh vb
    vagrant destroy vb
