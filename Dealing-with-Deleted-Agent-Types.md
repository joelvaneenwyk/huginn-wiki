If you receive the an `Agent(s) are 'missing in action'` error, you may want to understand how Agent types can be removed from Huginn.

There are a couple of ways that this can happen:

1. You may have updated to a newer version of Huginn that no longer contains an Agent type that you were using. Agents are sometimes removed from the Huginn codebase due to their deprecation (as with the BeeperAgent, since beeper.io no longer exists). Agents are also sometimes moved out of the Huginn codebase and into an Agent gem.
1. If the respective Agent is distributed as a Ruby gem, you may have accidentally removed it from the `ADDITIONAL_GEMS` environment setting.

For more about Agent gems, see <a href="https://github.com/cantino/huginn_agent" target="_blank">https://github.com/cantino/huginn_agent</a>.

## Agents that have been removed from Huginn

* BeeperAgent (service no longer exists)