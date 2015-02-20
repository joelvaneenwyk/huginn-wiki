So you've written an awesome agent that generates an event whenever a meteorite is scheduled to hit Earth. But meteorite strikes are relatively rare, so how do you go about testing your agent to see if it's actually working? Here are some tips:

* Take a look at `huginn/log/development.log` for **[what in particular gets logged here?]**
* From the web interface, run the agent manually (Actions -> Run) and look **[where for output?]**
* The Logs tab of each agent shows you everything the agent outputs **[via log? [like this?](https://github.com/cantino/huginn/blob/master/app/models/agents/imap_folder_agent.rb#L294)]**, including errors **[is this true in general?]**
* Use a ManualEvent agent to craft an event by hand and force your network of agents to run

TODO:
* Say something about the logging conventions and tools (e.g. what's the difference between `log` and `errors.add()`?)