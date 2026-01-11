# Python_AI Agents with Hugging Face smolagents2
---
### Let Agents Search the Web
Your friend wants to send $500 to her sister in New York but isn't sure if the exchange rate is still favorable. She remembers seeing “1 GBP → 1.24 USD” last week, but exchange rates can change daily.

To help her make a smart decision, you decide to build a code agent that can:

* Look up live GBP -> USD rate
* Summarize how the rate has changed over the past 7 days
* You'll give your agent web search powers using the built-in VisitWebpageTool.

Note: The model has been initialized for you. The CodeAgent class has been imported as well.
* Import the VisitWebpageTool from the smolagents library.
* Create the agent using the provided model and a tools list that includes an instance of VisitWebpageTool().
* Run the agent using the .run() method and pass in the task.
```
Hint
The tool you need is called VisitWebpageTool. It comes from the smolagents library.
Make sure to instantiate the tool (VisitWebpageTool()) and include it inside a list.
To run the agent, use .run(...) with your task string.
```
```python
# Import the VisitWebpageTool class
from smolagents import VisitWebpageTool

# Create agent with web search capabilities
agent = CodeAgent(
    tools=[VisitWebpageTool()],
    model=model
)

task = "Find GBP to USD exchange rates and summarize how this rate has changed over the past 7 days. A good source is usually Wise."

# Run the agent with the task
result = agent.run(task)
```
