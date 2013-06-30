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
      { :zipcode => "94103" }
    end

    def validate_options
      errors.add(:base, "zipcode is required") unless options[:zipcode].present?
    end

# Scheduling

Agents can be scheduled to run at certain times, or on certain intervals.  When a schedule is triggered, the `check` method in your Agent will be called.  If your agent should be schedulable, use the `default_schedule` class method to declare a default, otherwise you should call `cannot_be_scheduled!`.  Possible schedules are: `every_2m`, `every_5m`, `every_10m`, `every_30m`, `every_1h`, `every_2h`, `every_5h`, `every_12h`, `every_1d`, `every_2d`, `every_7d`, `midnight`, `1am`, `2am`, `3am`, `4am`, `5am`, `6am`, `7am`, `8am`, `9am`, `10am`, `11am`, `noon`, `1pm`, `2pm`, `3pm`, `4pm`, `5pm`, `6pm`, `7pm`, `8pm`, `9pm`, `10pm`, and `11pm`

    default_schedule "8pm"

    def check
      wunderground.forecast_for(options[:zipcode])["forecast"]["simpleforecast"]["forecastday"].each do |day|
        if is_tomorrow?(day)
          create_event :payload => day.merge(:zipcode => options[:zipcode])
        end
      end
    end

If your Agent creates events, as this example from the [WeatherAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/weather_agent.rb) does, then you should use the `event_description` class method to detail what data those events contain.

    event_description <<-MD
      Events look like this:

          {
            :zipcode => 12345,
            ...
            :maxhumidity => 93,
            :minhumidity => 63
          }
    MD

# Receiving Events

If your Agent can receive events, define a method called `receive` that accepts an array of incoming events.  Otherwise, please call `cannot_receive_events!`

# Memory

Agents have memory that can be used to maintain state between scheduled intervals or received events.  It will be loaded and saved automatically for you and is available in `memory`.

# Is it working?

It's nice to be able to tell the user if their instance of your Agent is working correctly.  You should define a method called `working?` that returns true when everything seems good.

    def working?
      (event = event_created_within(2.days)) && event.payload.present?
    end

# UI

Agents can have a custom UI by defining a show view at: `app/views/agents/agent_views/<agent name>/_show.html.erb`.