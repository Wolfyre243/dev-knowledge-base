Characteristics:
- AI model
- Defined set of tools
- Comprehensive system prompt

The above characteristics allow the system to autonomously handle user requests to complete specific tasks.

The agent is relying on the model's reasoning capabilities to interpret user requests and henceforth plan a sequence of steps to decide which tools to use from the defined set.

The system prompt will shape the agent's behaviour and define its core task, persona and operations, as well as the specific conditions for using each tool.

### Drawbacks
A single agent's performance can be less effective when it uses more tools and when its tasks increase in complexity. Symptoms can include increased latency, incorrect tool selection/use, or a failure to complete the task and see it through.

The issues mentioned above can be mitigated by refining the reasoning process of the agent, using techniques like the Reason and Act (ReAct) pattern.