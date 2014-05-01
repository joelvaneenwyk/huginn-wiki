**WARNING:** this is still in development and not yet available in the master branch of huginn.

### Liquid

Liquid is a template engine developed by [Shopify](http://shopify.com), it was designed to have a simple markup and to be non evaluating and secure. You can read more about it at it's [homepage](http://liquidmarkup.org/) or the GitHub [repository](https://github.com/Shopify/liquid/).

### Basic usage of Liquid in Huginn

For some simple examples have a look at the [HipChat](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/hipchat_agent.rb) or [Pushbullet](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/pushbullet_agent.rb) agents. Given the payload of the event your agents consumes is a hash with just one key named `message` you would just need to write `{{message}}` to dynamically use the value of this key.

To format the output you can use filters, they basically work like UNIX pipes: {{ mixed_case | downcase }}, which will return a down case version of the provided string.
For a complete list of build-in filters have a look at the documentation at [Shopify](http://docs.shopify.com/themes/liquid-basics/output).

### Filters added by Huginn

**uri_escape** returns a URI escaped string, useful when generating URL query strings 

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