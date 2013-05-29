Make sure you have [Vagrant](http://www.vagrantup.com/) installed.  Install [VirtualBox](https://www.virtualbox.org/) if you'd like to use it for testing, and/or setup an EC2 account for deployment.

Move to your Huginn directory in the Terminal.

Install librarian-chef gem

    gem install librarian-chef

And Vagrant plugins

    vagrant plugin install vagrant-aws
    vagrant plugin install vagrant-omnibus

Install the cookbooks mentioned in the Cheffile by running:

    cd deployment && librarian-chef install

To install Huginn on a VirtualBox virtual machine:

    vagrant up vb

The second case tells Vagrant to launch a VirtualBox virtual machine and install Huginn on it. You should now be able to visit `http://localhost:3000` to use Huginn on your local computer.

To install Huginn on AWS, edit the Vagrantfile and fill in your account details, then run

    vagrant up ec2 --provider=aws

Now you can point your browser to public DNS of the EC2 server in order to access it. Huginn will be at `/home/huginn/huginn`. A new user called `huginn` will be created with username `huginn` and password `huginn`. To ssh into ec2: 

    vagrant ssh ec2

Similarly, to ssh into VirtualBox

    vagrant ssh vb
    
After ssh-ing into ec2, you can start (its already running), stop, or restart Huginn with these commands:
    
    sudo start huginn
    sudo stop huginn
    sudo restart huginn

To terminate your EC2 instance:

    vagrant destroy ec2

Similarly, to destroy your VirtualBox virtual machine:

    vagrant destroy vb