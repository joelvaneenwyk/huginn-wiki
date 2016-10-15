**Problem**: Certain sites have ugly source code and/or render the page using JavaScript, making it next to impossible to use the WebsiteAgent. (Described in issue #888)

**Solution**: use [fulldom-server][] to run the JavaScript, allowing the DOM to build, then scrape the full DOM of the _actual_ page that appears after JS is run.

Note that using fulldom-server is significantly easier and simpler than [doing this with PhantomJS Cloud][phantomjs-cloud], but it _does_ require shell access to a server. If you don't have that, you'll probably have to stick with PhantomJS Cloud.

## Step 1 - installation

You need to have Node.js and npm installed. On a Debian-based system you can do this with, for example:

    $ sudo apt install nodejs nodejs-legacy
    $ curl -L curl https://npmjs.com/install.sh > npm-install.sh # npm is packaged but you're better off installing from upstream
    $ less npm-install.sh # It's always a good idea to make sure install scripts aren't doing anything nasty
    $ sudo bash npm-install.sh

Now that you have Node, you can install fulldom-server:

    $ sudo npm install -g fulldom-server

npm will spew a bunch of output and presto - you're done!

## Step 2 - running fulldom-server

You can start fulldom-server with no arguments, and it'll start up with some sensible defaults:

    $ fulldom-server
    Copyright (C) 2016 Alex Jordan <alex@strugee.net>.
    License AGPLv3+: GNU Affero GPL version 3 or later <http://gnu.org/licenses/agpl-3.0.html>.
    This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.
    Server listening at http://0.0.0.0:8000/

Note the part where it says it's listening on port 8000 on all interfaces (that's what `0.0.0.0` means).

If you want, you can have it listen only on localhost, on a different port, etc. How to do so is thoroughly documented [in the README][readme-config] and in `fulldom-server(1)`, which you can access by executing `man fulldom-server`.

## Step 2b - running fulldom-server all the time

You probably want to have fulldom-server running all the time, so you don't have to keep your terminal open running it in order for your agents to work. How to do so will vary by init system. On a systemd system, for example, you might put the following at `/etc/systemd/system/fulldom.service`:

```systemd
[Unit]
Description=proxy-like server that will show you the DOM of a page after JS runs
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/fulldom-server
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

Then have it start immediately as well as during boot with:

    $ sudo systemctl start fulldom
    $ sudo systemctl enable fulldom

## Step 3 - configuring WebsiteAgent

Last, you need to configure WebsiteAgent to use fulldom-server. Doing so is easy: all you do is [percent-encode your URLs][percent-encoding] - here's [a decent tool][encoding-tool] for this - then in your WebsiteAgent, put the URL to your fulldom-server instance, then `/`, then your percent-encoded URL.

However, this isn't quite enough. fulldom-server needs a hint to help it guess when the page is finished loading. So just append `?selector=` and whatever selector you're scraping to the end of the URL, ~~and you're done!~~ and you should be done, but this doesn't actually work due to [this issue][slash-issue]. Soon though!

 [fulldom-server]: https://github.com/strugee/fulldom-server
 [phantomjs-cloud]: https://github.com/cantino/huginn/wiki/Browser-Emulation-Using-PhantomJS-Cloud
 [readme-config]: https://github.com/strugee/fulldom-server#running
 [percent-encoding]: https://en.wikipedia.org/wiki/Percent-encoding
 [encoding-tool]: http://www.url-encode-decode.com/
 [slash-issue]: https://github.com/cantino/huginn/issues/1735
