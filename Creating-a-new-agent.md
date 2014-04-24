*Please note: Huginn's API is evolving and at some point Agents will likely be extracted into Ruby Gems.  We'd very much like your input into how this should work and what should be changed in this API.*

Huginn's Agents can create and receive events, and can be scheduled to run code at certain times or intervals.  Creating a new Huginn Agent is not difficult, you simply create a new subclass of Agent which defines a set of required methods.

# Description

Use the `description` class method to set a Markdown description for your agent.  For example:

    description <<-MD
      The WeatherAgent creates an event for the following day's weather at `zipcode`.

      You must setup an API key for Wunderground in order to use this Agent.
    MD

# Options

Agents are configured with a JSON structure from the user, symbolized and accessible via `options`.  You should define a method called `default_options` that returns an example default configuration for your type of Agent.  Additionally, you should define a method called `validate_options` that performs Rails validation on the contents of `options`, if any fields are required.  For example:

    def default_options
      { 'zipcode' => '94103' }
    end

    def validate_options
      errors.add(:base, 'zipcode is required') unless options['zipcode'].present?
    end

# Scheduling

Agents can be scheduled to run at certain times, or on certain intervals.  When a schedule is triggered, the `check` method in your Agent will be called.  If your agent should be schedulable, use the `default_schedule` class method to declare a default, otherwise you should call `cannot_be_scheduled!`.  Possible schedules are: `every_1m`, `every_2m`, `every_5m`, `every_10m`, `every_30m`, `every_1h`, `every_2h`, `every_5h`, `every_12h`, `every_1d`, `every_2d`, `every_7d`, `midnight`, `1am`, `2am`, `3am`, `4am`, `5am`, `6am`, `7am`, `8am`, `9am`, `10am`, `11am`, `noon`, `1pm`, `2pm`, `3pm`, `4pm`, `5pm`, `6pm`, `7pm`, `8pm`, `9pm`, `10pm`, and `11pm`

    default_schedule "8pm"

    def check
      wunderground.forecast_for(options['zipcode'])['forecast']['simpleforecast']['forecastday'].each do |day|
        if is_tomorrow?(day)
          create_event :payload => day.merge('zipcode' => options['zipcode'])
        end
      end
    end

If your Agent creates events, as this example from the [WeatherAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/weather_agent.rb) does, then you should use the `event_description` class method to detail what data those events contain.

    event_description <<-MD
      Events look like this:

          {
            'zipcode' => 12345,
            ...
            'maxhumidity' => 93,
            'minhumidity' => 63
          }
    MD

# Receiving Events

If your Agent can receive events, define a method called `receive` that accepts an array of incoming events.  Otherwise, please annotate it with a call to `cannot_receive_events!`.

# Creating Events

In code, your Agent can create events with `create_event :payload => { ... }`.  If your Agent will never create events, please annotate it with a call to `cannot_create_events!`.

# Memory

Agents have memory that can be used to maintain state between scheduled intervals or received events.  It will be loaded and saved automatically for you and is available in `memory`.

# Logging

Your Agent should create AgentLogs when interesting things happen, especially errors.  Call `log` or `error` with a log message and, optionally, `:outbound_event` or `:inbound_event` to keep track of events tied to the log message.

# Is it working?

It's nice to be able to tell the user if their instance of your Agent is working correctly.  You should define a method called `working?` that returns true when everything seems good.  Here's an example for an Agent that primarily creates events and has an `expected_update_period_in_days` option:

    def working?
      event_created_within?(options['expected_update_period_in_days']) && !recent_error_logs?
    end

And here is an example for an Agent that primarily receives events and has an `expected_receive_period_in_days` option:

    def working?
      last_receive_at && last_receive_at > options['expected_receive_period_in_days'].to_i.days.ago && !recent_error_logs?
    end

You can, of course, write Agent-specific code in `working?`.

# UI

Agents can have a custom UI by defining a show view at: `app/views/agents/agent_views/<agent name>/_show.html.erb`.  If they need to have server-side functionality, you may POST data to the `handle_details_post_agent_path` and handle it with `handle_details_post` in your Agent.  See the [ManualEventAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/manual_event_agent.rb) and its [details view](https://github.com/cantino/huginn/blob/master/app/views/agents/agent_views/manual_event_agent/_show.html.erb) for an example.

# Receiving Web Requests

Your Agent can receive web requests by implementing `receive_web_request`.  The URL for your Agent will be something like `http://yourserver.com/users/:user_id/web_requests/:agent_id/:secret` where `:user_id` is a User's id, `:agent_id` is an Agent's id, and `:secret` is a token that should be user-specifiable in your Agent's configuration and checked by `receive_web_request`. It is highly recommended that every Agent verify this token whenever `receive_web_request` is called. For example, one of your Agent's options could be `secret` and you could compare this value to `params[:secret]` whenever `receive_web_request` is called on your Agent, rejecting invalid requests.

Your Agent's `receive_web_request` method should return an Array containing a response, a status code, and an optional MIME type.  For example:

    [{ status: "success" }, 200]

or

    ["not found", 404, 'text/plain']

Here is an example implementation of `receive_web_request`:

```ruby
def receive_web_request(params, method, format)
  secret = params.delete('secret')
  return ["Please use POST requests only", 401] unless method == "post"
  return ["Not Authorized", 401] unless secret == options['secret']

  # do something with params here

  ['Done!', 200, 'text/plain']
end
```

Please see the [WebRequestsController](https://github.com/cantino/huginn/blob/master/app/controllers/web_requests_controller.rb) for more documentation, as well as the implementations of `receive_web_request` in [WebhookAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/webhook_agent.rb) and [DataOutputAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/data_output_agent.rb).