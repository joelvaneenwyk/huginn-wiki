If your SMTP password includes "special" characters (such as #, &, $, etc.), you should surround it with quotes like this:

SMTP_PASSWORD="My$Password#With&SpecialChars"

If not, you could see an error message in your logs like this one:

> Exception during check. end of file reached: /usr/lib/ruby/2.2.0/net/protocol.rb:153:in `read_nonblock' /usr/lib/ruby/2.2.0/net/protocol.rb:153:in `rbuf_fill' /usr/lib/ruby/2.2.0/net/protocol.rb:13...