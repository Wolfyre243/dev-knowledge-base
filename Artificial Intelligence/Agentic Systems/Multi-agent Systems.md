A multi-agent system orchestrates multiple specialised agents to solve complex problems that a single agent can't manage.

The core principle of a Multi-agent system is to decompose a large objective into smaller sub-tasks and assign each sub-task to a dedicated agent with a specific skill.

These agents then interact via collaborative/hierarchical workflows to achieve the final goal.

### Context Engineering
Each agent in a multi-agent system requires a specific context to perform its task effectively.

This is where context engineering comes in. 
Context can include:
- Documentation
- Historical Preferences
- Relevant Links
- Conversational History
- Operational Constraints

Strategies for context engineering include isolating context for a specific agent, persisting information across multiple steps, or compressing large amounts of data to improve efficiency.

# Sequential Pattern
In this pattern, we execute a series of specialised agents in a predefined, linear order where the output from an agent serves as the direct input for the next agent.

This pattern is rigid and preferred for pipelines with a predefined structure, such as a data processing pipeline that extracts data, cleans it and loads the data into a database, with 3 separate subagents for each task and 1 main agent that operates on predefined logic.

# Parallel Pattern
This pattern features multiple specialised subagents performing tasks/sub-tasks independently at the same time. The outputs of the subagents are then synthesized to produce the final consolidated response.

There is a parallel agent in the loop, and it does not have to consult another AI model to orchestrate its subagents. This means it can directly manage how and when the other agents run on its own.

Compared to the sequential pattern, this pattern can reduce overall latency since subagents run concurrently. However, this can increase immediate resource utilisation and introduce more operational costs. Complexity also arises when more logic is needed to synthesize potentially conflicting results.

# Loop Pattern
This pattern repeatedly executes a sequence of specialised subagents, basically like the sequential pattern in a while loop.

The loop workflow agent in this pattern operates on its own predefined logic without consulting an AI model for orchestration. Once all its subagents are done with their tasks, the loop agent evaluates the final output and determines whether an exit condition is met.
If the condition has not been met, the loop agent starts the sequence of subagents again.

The loop pattern allows us to build complex, iterative workflows that enable agents to refine their work until a specific quality is met. The biggest trade-off in this pattern is the risk of an infinite loop, if termination conditions are not properly defined or if the subagents fail to produce the state required to stop repeatedly. This leads to excessive operational costs and potential system hangs.

# Review and Critique Pattern
This pattern focuses on improving quality and reliability of generated content by using two specialised agents, typically in a sequential flow. This pattern is an implementation of the [[#Loop Pattern | loop pattern]].

A generator agent creates an initial output, such as a block of code or a summary of a document. The critic agent then evaluates this output based on a predefined set of criteria, and approves or rejects the content with feedback for revision.

The review and critique pattern can improve output quality and accuracy. However, this also comes at the direct cost of increased latency and operational cost.

# Iterative Refinement Pattern
This pattern uses a looping mechanism to progressively improve an output over multiple cycles. It is an implementation of the [[#Loop Pattern|loop pattern]].

This pattern is very similar to the loop pattern itself, but varies in its self-improvement nature. Agents work within the loop to modify a result stored in the session state during each iteration, until the output meets a predefined quality threshold (or a maximum number of iterations).

The iterative refinement pattern can produce highly complex or polished outputs that would be difficult to achieve in a single step, but the looping mechanism directly increases latency and operational costs per cycle.

# Coordinator Pattern
This pattern uses a central agent known as the coordinator to direct a workflow. The coordinator analyses and decomposes a user's request into sub-tasks. It then dispatches these sub-tasks to specialised agents for execution.

In this pattern, each specialised agent has a specific function (e.g. querying a database, calling an API). This pattern uses an AI model to orchestrate and **dynamically route tasks**, which is a huge distinction between other patterns with predefined workflows.

The coordinator pattern offers much more flexibility compared to more rigid and predefined workflows. By using a model to dynamically route tasks, the coordinator can handle a wide variety of inputs and adapt to multiple scenarios. However, this pattern will result in more model calls which can increase token throughput and lead to higher operational costs. 

# Hierarchical Task Decomposition Pattern
This pattern organises agents into a multi-level hierarchy to solve complex problems that require extensive planning. A top-level parent known as the Root Agent receives a complex task and is responsible for decomposing the task into smaller manageable sub-tasks.

The root agent may delegate a sub-task to a specialised subagent at a lower level, spawning another layer of subagents. This process can repeat through multiple layers, with agents that progressively decompose their assigned tasks until the tasks are simple enough for a worker agent at the lowest level to execute directly.

The hierarchical task decomposition pattern is ideal for solving highly complex problems where systematic decomposition is needed. However, this will then introduce significant trade-offs due to its obvious architectural complexity.