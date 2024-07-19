This document describes how to install Huginn on a Fedora 20 machine. This tutorial should probably work on Centos 7, but was not tested.

## Install System Dependencies

`sudo yum install -y ruby ruby-devel rubygem-bundler rubygem-rake mysql-server mysql-devel gcc gcc-c++ git`

# Get huginn

- `git clone https://github.com/cantino/huginn.git`
- `cd huginn`

## Install Huginn's Rubygems dependencies

- `bundle install`

## Start the MySQL server:

- `sudo service mysqld start`

- If you want to start MySQL on boot `sudo systemctl enable mariadb.service`

## Finalizing install

- Copy .env.example\* to .env: `cp .env.example .env`

- Initialize the Huginn and database: `./bin/rake secret db:create db:migrate`

## Start

`./bin/rails s`
