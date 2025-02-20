# Novice Setup Guide

Written by a Ruby novice for those who are clueless during set up as well. These instructions are for Linux.

Note: It's _much_ easier to get the project setup and going on Linux than Windows. If you're on Windows, grab a [Linux VM ](http://www.osboxes.org/) for [VMWare Player](https://www.vmware.com/products/player) or [Virtual Box](https://www.virtualbox.org/) and follow the instructions below.
If you're on a Mac, view revised guide [here](https://github.com/huginn/huginn/wiki/Novice-Setup-Guide-for-Mac).

There is also a (very verbose) [OpenSUSE 13.2 install guide](https://github.com/huginn/huginn/wiki/OpenSUSE-13.2---From-distro-install-to-installed-Huginn).

## Step 1 - Clone the repository

Since you are on GitHub, you have probably done this step a thousand times before.

Verify you have [git][git] installed on your machine, go to a directory where you would like to work, and clone the repository.

[git]: http://git-scm.com/

```shell
git clone git://github.com/huginn/huginn.git
```

### Troubleshooting

If you fail to clone the repository because of environment issue to block git protocol, retry it again after '.gitconfig in your home folder' is changed

```shell
[url "https://github.com"]
      insteadof = git://github.com
```

## Step 2 - Install ruby and gem

Install [ruby][ruby] (2.6.x) and [gem][gem]. You can either download them and compile manually or install via your OS' package manager (e.g. [homebrew][homebrew] for Mac OS X or [apt][apt] for Ubuntu). We recommend using [rvm](http://rvm.io/) or [rbenv](https://github.com/sstephenson/rbenv). You will also need MySQL or Postgres, both of which can also be installed via your package manager.

[ruby]: http://www.ruby-lang.org/en/
[gem]: http://rubygems.org/
[apt]: http://linux.die.net/man/8/apt-get
[homebrew]: http://brew.sh

## Step 3 - Install rake and bundler

Now that we have [gem][gem] installed, we can install [rake][rake], the ruby build utility, and [bundler][bundler], the ruby gem dependency manager. You shouldn't need to do this step if you're using rvm or rbenv.

```shell
gem install rake bundler
```

[rake]: http://rake.rubyforge.org/
[bundler]: http://gembundler.com/

## Step 4 - Install local dependencies

As mentioned, [bundler][bundler] helps to manage dependencies. Verify you are in the cloned `huginn` directory. Run `bundle` to install Huginn's dependencies.

```shell
bundle
```

### Troubleshooting

#### mysql2

If you receive an error like the one below, you have failed to install the [mysql2][mysql2] gem. Continue reading after the error message.

[mysql2]: https://github.com/brianmario/mysql

```
Building native extensions.  This could take a while...
ERROR:  Error installing mysql2:
  ERROR: Failed to build gem native extension.

        /usr/bin/ruby1.9.1 extconf.rb
checking for rb_thread_blocking_region()... yes
checking for rb_wait_for_single_fd()... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lm... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lz... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lsocket... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lnsl... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lmygcc... no
checking for mysql_query() in -lmysqlclient... no
*** extconf.rb failed ***
```

You must install the [proper dependencies][mysql2-deps] for [mysql2][mysql2]. One of the following commands will install them on Ubuntu (not all commands will run/find a package):

```shell
apt-get install libmysqlclient-dev
apt-get install mysql-devel
```

[mysql2-deps]: https://github.com/brianmario/mysql2#installing

Once you have installed the dependencies, you can install [mysql2][mysql2] individually via `gem install mysql2`. After it installs, re-run `bundle`.

## Step 5 - Install and start mysql-server

Install [mysql-server][mysql-server] and start it up (`apt-get` will automatically start the process).

[mysql-server]: https://launchpad.net/mysql-server

```shell
apt-get install mysql-server
```

## Step 6 - Follow the rest of Quick Start

From here on, the [Getting Started][getting-started] section of the [README][README] should be able to guide you.

[getting-started]: https://github.com/huginn/huginn#getting-started
[README]: https://github.com/huginn/huginn#readme
