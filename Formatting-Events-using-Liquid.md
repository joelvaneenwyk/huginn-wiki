### Liquid

Liquid is a template engine developed by [Shopify](http://shopify.com), it was designed to have a simple markup and to be non evaluating and secure. You can read more about it at it's [homepage](http://liquidmarkup.org/) or the GitHub [repository](https://github.com/Shopify/liquid/).

### Basic usage of Liquid in Huginn

For some simple examples have a look at the [HipChat](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/hipchat_agent.rb) or [Pushbullet](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/pushbullet_agent.rb) agents. Given the payload of the event your agents consumes is a hash with just one key named `message` you would just need to write `{{message}}` to dynamically use the value of this key.

To format the output you can use filters, they basically work like UNIX pipes:  
{{ 'hello' | [replace: 'hello', 'hi'](https://docs.shopify.com/themes/liquid-documentation/filters/string-filters#replace) | [upcase](https://docs.shopify.com/themes/liquid-documentation/filters/string-filters#upcase) }} would output 'HI'.

For a complete list of build-in filters have a look at the documentation at [Shopify](http://docs.shopify.com/themes/liquid-basics/output).

### Objects provided by Huginn

#### Event

An Event object is essentially a hash created by an upstream Agent.  There are also some special keys listed below, which are available unless the hash has keys with the same name.

**\_location_** contains location information bound to the event, which has the following keys: `latitude` (alias `lat`), `longitude` (alias `lng`), `radius`, `course` and `speed`.  This is set by some agents that deal with location.

**agent** refers to the upstream Agent which created the Event.

**created_at** refers to the timestamp of the Event.

#### Agent

An Agent object has the following keys (excerpt).

**type** returns the type name, e.g. `"HipchatAgent"`.

**name** returns the name.

**options** returns the options hash.

**memory** returns the memory hash.

**sources** returns an array of the upstream Agents.

**receivers** returns an array of the downstream Agents.

**disabled** returns a boolean value that indicates if the Agent is in a disabled state.

### Filters added by Huginn

**uri_escape** returns a URI escaped string, useful when generating URL query strings.
<!-- Liquid 3 will have url_encode which is equivalent to this -->

**to_uri** parses an input into a URI object, optionally resolving it against a base URI if given.

A URI object will have the following properties: `scheme`, `userinfo`, `host`, `port`, `registry`, `path`, `opaque`, `query`, and `fragment`.  You'll have to "assign" the result to a variable in order to access these properties.

**uri_expand** returns the destination URL of a given URL by recursively following redirects, up to 5 times in a row.
If a given string is not a valid absolute HTTP URL or in case of too many redirects, the original string is returned.
If any network/protocol error occurs while following redirects, the last URL followed is returned.

e.g. When a variable `short_url` contains a URL "https://goo.gl/tfDrI", `{{ short_url | uri_expand }}` expands to "https://github.com/cantino/huginn".

**to_xpath** returns an XPath literal or expression that evaluates to the original string for use in WebsiteAgent.

For example, suppose you are making a WebsiteAgent that receives an event with a `word` to look up on a glossary web page to create a new event.
It would have to dynamically build an XPath expression like this:

    //dl/dt[text()={{word | to_xpath}}][1]/following-sibling::dd[1]/text()

It is more robust to use the filter here than to put `'{{word}}'` or `"{{word}}"` in that it wouldn't blow up the whole expression even if `word` contained the apostrophe, quotation mark, or both.

### Tags added by Huginn

**credential** returns the stored user credential for the given credential name. Usage: `{% credential USER_CREDENTIAL_NAME %}`, note there are no back-quotes around the credential name; the name is case sensitive and has to match the store user credential name exactly.

**line_break** evaluates to a literal line break in the text, i.e. a \n character.  Usage: `{% line_break %}`; note that there are no quotes or back ticks around the tag.

### More complete usage example

In this example a HipchatAgent will consume events emitted by an BasecampAgent.

Basecamp events will look like this (trimmed down for better readability):
```
{
  "creator": {
    "name": "Dominik Sander",
  },
 "excerpt": "test test",
 "summary": "commented on whaat",
 "action": "commented on",
 "target": "whaat",
 "html_url": "https://basecamp.com/12456/projects/76454545-explore-basecamp/messages/76454545-whaat#comment_76454545"
}
```
Now we generate a nice HTML formatted message using Liquid. This is the HipchatAgent options hash:
```
{
  'auth_token' => 'token',
  'room_name' => 'test',
  'username' => "{{creator.name}}",
  'message' => '{{summary}}<br>{{excerpt}}<br><a href="{{html_url}}">View it on Basecamp</a>',
  'notify' => false,
  'color' => 'yellow',
}
```
