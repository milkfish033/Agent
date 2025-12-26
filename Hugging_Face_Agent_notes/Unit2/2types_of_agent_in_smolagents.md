# 1 Code Agent

Generate executable python code, has better performance overall


```
from smolagents import CodeAgent, InferenceClientModel
import numpy as np
import time
import datetime

agent = CodeAgent(tools=[], model=InferenceClientModel(), additional_authorized_imports=['datetime'])

agent.run(
    """
    Alfred needs to prepare for the party. Here are the tasks:
    1. Prepare the drinks - 30 minutes
    2. Decorate the mansion - 60 minutes
    3. Set up the menu - 45 minutes
    3. Prepare the music and playlist - 45 minutes

    If we start right now, at what time will the party be ready?
    ""
    )
```


# 2 Tool Calling Agent 

Tool Calling Agents follow the same multi-step workflow as Code Agents (see the previous section for details).

The key difference is in how they structure their actions: instead of executable code, they generate JSON objects that specify tool names and arguments. The system then parses these instructions to execute the appropriate tools.

```
from smolagents import ToolCallingAgent, WebSearchTool, InferenceClientModel

agent = ToolCallingAgent(tools=[WebSearchTool()], model=InferenceClientModel())

agent.run("Search for the best music recommendations for a party at the Wayne's mansion.")
```

output:
```
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Calling tool: 'web_search' with arguments: {'query': "best music recommendations for a party at Wayne's         │
│ mansion"}                                                                                                       │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```