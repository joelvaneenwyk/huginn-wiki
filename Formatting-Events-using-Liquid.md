# Liquid

Liquid is a template engine developed by [Shopify](http://shopify.com), it was designed to have a simple markup and to be non evaluating and secure. You can read more about it at it's [homepage](https://shopify.github.io/liquid) or the GitHub [repository](https://github.com/Shopify/liquid/).

https://shopify.dev/docs/themes/liquid

### Basic usage of Liquid

For some simple examples have a look at the [HipChat](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/hipchat_agent.rb) or [Pushbullet](https://github.com/cantino/huginn/blob/07243cee345060316ff2b27530e20e38e72d7713/app/models/agents/pushbullet_agent.rb) agents. Given the payload of the event your agents consumes is a hash with just one key named `message` you would just need to write `{{message}}` to dynamically use the value of this key.

To format the output you can use filters, they basically work like UNIX pipes:  
`{{ 'hello' | replace: 'hello', 'hi' | upcase }}` would output `HI`.  
(See docs for [replace](https://shopify.github.io/liquid/filters/replace/), and [upcase](https://shopify.github.io/liquid/filters/upcase/).)

For a complete list of build-in filters have a look at the documentation at [Shopify](https://shopify.github.io/liquid/basics/introduction/).

## Objects provided by Huginn

### Event

An Event object is essentially a hash created by an upstream Agent. There are also some special keys listed below, which are available unless the hash has keys with the same name.

| Key          | Description                                                                                                                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `_location_` | contains location information bound to the event, which has the following keys: `latitude` (alias `lat`), `longitude` (alias `lng`), `radius`, `course` and `speed`. This is set by some agents that deal with location. |
| `agent`      | refers to the upstream Agent which created the Event.                                                                                                                                                                    |
| `created_at` | refers to the timestamp of the Event.                                                                                                                                                                                    |

### Agent

An Agent object has the following keys (excerpt).

| Key         | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| `type`      | returns the type name, e.g. `"HipchatAgent"`.                               |
| `name`      | returns the name.                                                           |
| `options`   | returns the options hash.                                                   |
| `memory`    | returns the memory hash.                                                    |
| `sources`   | returns an array of the upstream Agents.                                    |
| `receivers` | returns an array of the downstream Agents.                                  |
| `disabled`  | returns a boolean value that indicates if the Agent is in a disabled state. |

## Filters added by Huginn

| Filter                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `uri_escape`                            | returns a URI escaped string, useful when generating URL query strings.                                                                                                                                                                                                                                                                                                                                                                                                |
| `to_uri`                                | parses an input into a URI object, optionally resolving it against a base URI if given.                                                                                                                                                                                                                                                                                                                                                                                |
| `rebase_hrefs`                          | takes a fragment of HTML/XML and replaces all relative URL references in it with their absolute URLs, using a given URL as base.                                                                                                                                                                                                                                                                                                                                       |
| `uri_expand`                            | returns the destination URL of a given URL by recursively following redirects, up to 5 times in a row.                                                                                                                                                                                                                                                                                                                                                                 |
| `unescape`                              | unescapes (basic) HTML entities in a string. This currently decodes the following entities only: `&apos;`, `&quot;`, `&lt;`, `&gt;`, `&amp;`, `&#dd;` and `&#xhh;`.                                                                                                                                                                                                                                                                                                    |
| `to_xpath`                              | returns an XPath literal or expression that evaluates to the original string for use in a WebsiteAgent.                                                                                                                                                                                                                                                                                                                                                                |
| `regex_extract`                         | extract a matching substring found in a string. It takes a regex pattern followed by an optional group index. e.g. To capture a version number from a phrase `{% assign phrase = "Product version 1.0.5 has been released." %}`, try this: `{{ phrase \| regex_extract: "[\\d.]+" }}` or more specifically: `{{ phrase \| regex_extract: "version (?<ver>[\\d.]+)", "ver" }}` / `{{ phrase \| regex_extract: "version ([\\d.]+)", 1 }}` (New feature since 2023-02-19) |
| `regex_replace` & `regex_replace_first` | replace all/first regex matching strings with a substring. Very similar to the [built in replace](https://shopify.github.io/liquid/filters/replace/).                                                                                                                                                                                                                                                                                                                  |
| `json`                                  | takes the object provided and serializes it into a JSON string: `{{ data \| json }}`                                                                                                                                                                                                                                                                                                                                                                                   |
| `as_object`                             | Returns a Ruby object                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `group_by`                              | groups an array of items by a a property (analogous to `array.group_by(&:property_name)` in ruby)                                                                                                                                                                                                                                                                                                                                                                      |

### Details

#### `to_uri`

A URI object will have the following properties: `scheme`, `userinfo`, `host`, `port`, `registry`, `path`, `opaque`, `query`, and `fragment`. You'll have to "assign" the result to a variable in order to access these properties.

#### `rebase_hrefs`

A typical use case is in the `template` option of a WebsiteAgent, where it takes an extracted HTML fragment to resolve relative references in it like this: `{{ content | rebase_hrefs: _request_.url }}`

#### `uri_expand`

If a given string is not a valid absolute HTTP URL or in case of too many redirects, the original string is returned.
If any network/protocol error occurs while following redirects, the last URL followed is returned.

e.g. When a variable `short_url` contains a URL "https://goo.gl/tfDrI", `{{ short_url | uri_expand }}` expands to "https://github.com/cantino/huginn".

#### `to_xpath`

For example, suppose you are making a WebsiteAgent that receives an event with a `word` to look up on a glossary web page to create a new event. It would have to dynamically build an XPath expression like this:

```xpath
//dl/dt[text()={{word | to_xpath}}][1]/following-sibling::dd[1]/text()
```

It is more robust to use the filter here than to put `'{{word}}'` or `"{{word}}"`, in that it wouldn't blow up the whole expression even if `word` contained the apostrophe, quotation mark, or both. You can also use this with the `_response_` object to do extract and escape some header, such as `{{ _response_.headers.Content-Type | to_xpath }}`.

#### `regex_replace` & `regex_replace_first`

For example, if `foobar` contains the string "foobaz foobaz", then `{{ foobar | regex_replace: '(\S+)baz', 'qux\1' }}` would result in "quxfoo quxfoo". You can use any regex supported by the Ruby `Regexp` class, as documented [here](http://ruby-doc.org/core/doc/regexp_rdoc.html).

You can use escape sequences in both the regex and the replacement parameters of these filter functions, such as `\t`, `\r`, `\n`, `\xXX` and `\u{XXXX}`. In the replacement parameter, numbered capture groups `\1`..`\9` are supported, as well as named capture groups `\k<name>`, `\&`, `` \` ``, `\'`, etc.

Beware that Liquid itself does not have the concept of backslash escaping, so you cannot escape quote characters like `"\""`. Instead, use `\x22` when you need to put the double quote character in a double quoted string literal, e.g. `{{ text | regex_replace: "\x22(.*?)\x22", "\1" }}`.

#### `as_object`

It can be used as a JSONPath replacement for Agents that only support Liquid:

```liquid
Event:   {"something": {"nested": {"data": 1}}}
Liquid:  {{something.nested | as_object}}
Returns: {"data": 1}
```

Splitting up a string with Liquid filters and return the Array:

```liquid
Event:   {"data": "A,B,C"}
Liquid:  {{data | split: ',' | as_object}}
Returns: ['A', 'B', 'C']
```

`as_object` ALWAYS has to be the last filter in a Liquid expression!

Note that `as_object` will explicitly cast an integer without the quotes when input that way, whereas normally integers would be output as strings by Liquid formatting. For example if in JSON you need to return an object in format `{ "id": 123 }` you would likely need to use as_object like `{ "id": {{item | as_object }} }`.
Using `{ "id": {{item}} }` would change the result to `{ "id": "123" }` perhaps unexpectedly.

#### `group_by`

Example usage:

```liquid
{% assign posts_by_author = site.posts | group_by: "author" %}
{% for author in posts_by_author %}
    <dt>{{author.name}}</dt>
    {% for post in author.items %}
        <dd><a href="{{post.url}}">{{post.title}}</a></dd>
    {% endfor %}
{% endfor %}
```

## Tags added by Huginn

| Tag                                     | Description                                                                                                                                                           |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `credential`                            | returns the stored user credential for the given credential name.                                                                                                     |
| `line_break`                            | evaluates to a literal line break in the text, i.e. a \n character.                                                                                                   |
| `regex_replace` & `regex_replace_first` | replace every occurrence of a given regex pattern in the first "in" block with the result of the "with" block in which the variable `match` is set for each iteration |

### Details

#### `credential`

Usage: `{% credential USER_CREDENTIAL_NAME %}`

Note: there are no back-quotes around the credential name; the name is case sensitive and has to match the store user credential name exactly.

#### `line_break`

Usage: `{% line_break %}`

Note: that there are no quotes or back ticks around the tag.  
(Note: for HTML emails, you may want to use `<br>` instead.)

#### `regex_replace` & `regex_replace_first`

Can be used as follows:

- `match[0]` or just `match`: the whole matching string
- `match[1]`..`match[n]`: strings matching the numbered capture groups
- `match.size`: total number of the elements above (n+1)
- `match.names`: array of names of named capture groups
- `match[name]`..: strings matching the named capture groups
- `match.pre_match`: string preceding the match
- `match.post_match`: string following the match
- `match.***`: equivalent to `match['***']` unless it conflicts with the existing methods above

If named captures (`(?<name>...)`) are used in the pattern, they are also made accessible as variables. Note that if numbered captures are used mixed with named captures, you could get unexpected results.

Example usage:

```liquid
{% regex_replace "\w+" in %}Use me like this.{% with %}{{ match | capitalize }}{% endregex_replace %}
{% assign fullname = "Doe, John A." %}
{% regex_replace_first "\A(?<name1>.+), (?<name2>.+)\z" in %}{{ fullname }}{% with %}{{ name2 }} {{ name1 }}{% endregex_replace_first %}

Use Me Like This.

John A. Doe
```

## More complete usage example

In this example a HipchatAgent will consume events emitted by an BasecampAgent.

Basecamp events will look like this (trimmed down for better readability):

```json
{
  "creator": {
    "name": "Dominik Sander"
  },
  "excerpt": "test test",
  "summary": "commented on whaat",
  "action": "commented on",
  "target": "whaat",
  "html_url": "https://basecamp.com/12456/projects/76454545-explore-basecamp/messages/76454545-whaat#comment_76454545"
}
```

Now we generate a nice HTML formatted message using Liquid. This is the HipchatAgent options hash:

```json
{
  "auth_token": "token",
  "room_name": "test",
  "username": "{{creator.name}}",
  "message": "{{summary}}<br>{{excerpt}}<br><a href='{{html_url}}'>View it on Basecamp</a>",
  "notify": false,
  "color": "yellow"
}
```

## More Examples

- Removing newlines from a string: `{{foo | strip_newlines}}`
- Handling dates in Liquid: Dates are stored as the number of seconds since the epoch (1st Jan 1970) and can be handled as an integer using Filters. For example, an integer variable `dateVar` which stores the date in milliseconds can be output as a formatted date string by first dividing by 1000, and then using Liquid's date formatting Filter as follows:

  ```liquid
  {{ dateVar | divided_by: 1000 | date: "%c" }}
  ```

  To insert the current date and time:

  ```liquid
  {{ 'now' | date: '%Y-%m-%d %H:%M:%S' }}
  ```

  Other readable date output formats are available, see the reference page: http://shopify.github.io/liquid/filters/date/

- See [this comment](https://github.com/cantino/huginn/issues/1589#issuecomment-234781489) for an example of extracting data in a loop.
- Limit the description of an RSS feed to 500 characters with the following code for the EventFormattingAgent:
  ```json
  {
    "instructions": {
      "title": "<a href=\"{{url}}\">{{title}}</a>",
      "description": "{{description | truncate: 500 }}"
    },
    "matchers": [],
    "mode": "clean"
  }
  ```
