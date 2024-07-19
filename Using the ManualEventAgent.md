One of the more useful tools Huginn includes for development and debugging of agent networks is the Manual Event Agent, which lets the developer craft events by hand and transmit them to other agents to be acted upon. The Manual Event Agent permits the user to precisely specify the contents of an event by writing it from scratch in the form of a JSON document of arbitrary size and complexity. Here is how to use it:

- Instantiate an instance of the Manual Event Agent. This can be within an existing Scenario or it can be free-standing.
- Wire the Manual Event Agent into the agent under testing or debugging. This is done by making the Manual Event Agent into an event source like any other. Remember that any agent can have more than event source.
- In the Agents list or Scenario Diagram, click on the Manual Event Agent. Then click on the Summary tab.
- In the Options box enter a JSON document which describes the event to send. This can be as simple as the following:

  {
  "message": "Hello, world!"
  }

- Click the Submit button. The manually created event will then propagate to the next agent in the chain.
