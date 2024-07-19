So you've written an awesome agent that generates an event whenever a meteorite hits the Earth. But last time a meteorite struck, something went wrong. Your agent didn't generate any events! What's the best way to debug, especially if you don't want to wait for another strike?

If you think your agent has a bug, try inserting a useful `log()` or `errors.add()` statement (either will do). Then use the web interface to run your agent manually (Actions -> Run), and check its Logs tab for messages (Actions -> Show -> Logs).

You can also use a ManualEvent agent to craft an event by hand and force an entire network of agents to run.

Finally, an accumulation of all logged messages and errors can be found in `huginn/log/development.log`, but this is usually harder to sift through than the Logs tab of an individual agent.

TODO:

- Explain the difference between `log()` and `errors.add()`
