# Why use smolagents


## What is `smolagents`?

`smolagents` is a simple yet powerful framework for building AI agents. It provides LLMs with the _agency_ to interact with the real world, such as searching or generating images.



### Key Advantages of `smolagents`
- **Simplicity:** Minimal code complexity and abstractions, to make the framework easy to understand, adopt and extend
- **Flexible LLM Support:** Works with any LLM through integration with Hugging Face tools and external APIs
- **Code-First Approach:** First-class support for Code Agents that write their actions directly in code, removing the need for parsing and simplifying tool calling 
- **HF Hub Integration:** Seamless integration with the Hugging Face Hub, allowing the use of Gradio Spaces as tools

### When to use smolagents?

With these advantages in mind, when should we use smolagents over other frameworks? 

smolagents is ideal when:
- You need a **lightweight and minimal solution.**
- You want to **experiment quickly** without complex configurations.
- Your **application logic is straightforward.**

### Code vs. JSON Actions
Unlike other frameworks where agents write actions in JSON, `smolagents` **focuses on tool calls in code**, simplifying the execution process. This is because there's no need to parse the JSON in order to build code that calls the tools: the output can be executed directly.

The following diagram illustrates this difference:

![Code vs. JSON actions](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/transformers/code_vs_json_actions.png)

To review the difference between Code vs JSON Actions, you can revisit [the Actions Section in Unit 1](https://huggingface.co/learn/agents-course/unit1/actions#actions-enabling-the-agent-to-engage-with-its-environment).

### Agent Types in `smolagents`

Agents in `smolagents` operate as **multi-step agents**. 

Each [`MultiStepAgent`](https://huggingface.co/docs/smolagents/main/en/reference/agents#smolagents.MultiStepAgent) performs:
- One thought
- One tool call and execution

In addition to using **[CodeAgent](https://huggingface.co/docs/smolagents/main/en/reference/agents#smolagents.CodeAgent)** as the primary type of agent, smolagents also supports **[ToolCallingAgent](https://huggingface.co/docs/smolagents/main/en/reference/agents#smolagents.ToolCallingAgent)**, which writes tool calls in JSON.

We will explore each agent type in more detail in the following sections.

> [!TIP]
> In smolagents, tools are defined using @tool decorator wrapping a Python function or the Tool class.

### Model Integration in `smolagents`
`smolagents` supports flexible LLM integration, allowing you to use any callable model that meets [certain criteria](https://huggingface.co/docs/smolagents/main/en/reference/models). The framework provides several predefined classes to simplify model connections:

- **[TransformersModel](https://huggingface.co/docs/smolagents/main/en/reference/models#smolagents.TransformersModel):** Implements a local `transformers` pipeline for seamless integration.
- **[InferenceClientModel](https://huggingface.co/docs/smolagents/main/en/reference/models#smolagents.InferenceClientModel):** Supports [serverless inference](https://huggingface.co/docs/huggingface_hub/main/en/guides/inference) calls through [Hugging Face's infrastructure](https://huggingface.co/docs/api-inference/index), or via a growing number of [third-party inference providers](https://huggingface.co/docs/huggingface_hub/main/en/guides/inference#supported-providers-and-tasks).
- **[LiteLLMModel](https://huggingface.co/docs/smolagents/main/en/reference/models#smolagents.LiteLLMModel):** Leverages [LiteLLM](https://www.litellm.ai/) for lightweight model interactions.
- **[OpenAIServerModel](https://huggingface.co/docs/smolagents/main/en/reference/models#smolagents.OpenAIServerModel):** Connects to any service that offers an OpenAI API interface.
- **[AzureOpenAIServerModel](https://huggingface.co/docs/smolagents/main/en/reference/models#smolagents.AzureOpenAIServerModel):** Supports integration with any Azure OpenAI deployment.

This flexibility ensures that developers can choose the model and service most suitable for their specific use cases, and allows for easy experimentation.

### Inspecting Our Party Preparator Agent with OpenTelemetry and Langfuse 📡

As Alfred fine-tunes the Party Preparator Agent, he's growing weary of debugging its runs. Agents, by nature, are unpredictable and difficult to inspect. But since he aims to build the ultimate Party Preparator Agent and deploy it in production, he needs robust traceability for future monitoring and analysis.  

Once again, `smolagents` comes to the rescue! It embraces the [OpenTelemetry](https://opentelemetry.io/) standard for instrumenting agent runs, allowing seamless inspection and logging. With the help of [Langfuse](https://langfuse.com/) and the `SmolagentsInstrumentor`, Alfred can easily track and analyze his agent’s behavior.  

Setting it up is straightforward!  

First, we need to install the necessary dependencies:  

```bash
pip install opentelemetry-sdk opentelemetry-exporter-otlp openinference-instrumentation-smolagents langfuse
```

Next, Alfred has already created an account on Langfuse and has his API keys ready. If you haven’t done so yet, you can sign up for Langfuse Cloud [here](https://cloud.langfuse.com/) or explore [alternatives](https://huggingface.co/docs/smolagents/tutorials/inspect_runs).  

Once you have your API keys, they need to be properly configured as follows:

```python
import os

# Get keys for your project from the project settings page: https://cloud.langfuse.com
os.environ["LANGFUSE_PUBLIC_KEY"] = "pk-lf-..." 
os.environ["LANGFUSE_SECRET_KEY"] = "sk-lf-..." 
os.environ["LANGFUSE_HOST"] = "https://cloud.langfuse.com" # 🇪🇺 EU region
# os.environ["LANGFUSE_HOST"] = "https://us.cloud.langfuse.com" # 🇺🇸 US region
```

With the environment variables set, we can now initialize the Langfuse client. get_client() initializes the Langfuse client using the credentials provided in the environment variables.

```python
from langfuse import get_client
 
langfuse = get_client()
 
# Verify connection
if langfuse.auth_check():
    print("Langfuse client is authenticated and ready!")
else:
    print("Authentication failed. Please check your credentials and host.")
```

Finally, Alfred is ready to initialize the `SmolagentsInstrumentor` and start tracking his agent's performance.  

```python
from openinference.instrumentation.smolagents import SmolagentsInstrumentor

SmolagentsInstrumentor().instrument()
```

Alfred is now connected 🔌! The runs from `smolagents` are being logged in Langfuse, giving him full visibility into the agent's behavior. With this setup, he's ready to revisit previous runs and refine his Party Preparator Agent even further. 

> [!TIP]
> To learn more about tracing your agents and using the collected data to evaluate their performance, check out Bonus Unit 2.

```python
from smolagents import CodeAgent, InferenceClientModel

agent = CodeAgent(tools=[], model=InferenceClientModel())
alfred_agent = agent.from_hub('sergiopaniego/AlfredAgent', trust_remote_code=True)
alfred_agent.run("Give me the best playlist for a party at Wayne's mansion. The party idea is a 'villain masquerade' theme")  
```

Alfred can now access these logs [here](https://cloud.langfuse.com/project/cm7bq0abj025rad078ak3luwi/traces/995fc019255528e4f48cf6770b0ce27b?timestamp=2025-02-19T10%3A28%3A36.929Z) to review and analyze them.  

> [!TIP]
> Actually, a minor error occurred during execution. Can you spot it in the logs? Try to track how the agent handles it and still returns a valid answer. Here is the direct link to the error if you want to verify your answer. Of course the error has been fixed in the meantime, more details can be found in this issue.

Meanwhile, the [suggested playlist](https://open.spotify.com/playlist/0gZMMHjuxMrrybQ7wTMTpw) sets the perfect vibe for the party preparations. Cool, right? 🎶  

---

Now that we have created our first Code Agent, let's **learn how we can create Tool Calling Agents**, the second type of agent available in `smolagents`.

## Resources

- [smolagents Blog](https://huggingface.co/blog/smolagents) - Introduction to smolagents and code interactions
- [smolagents: Building Good Agents](https://huggingface.co/docs/smolagents/tutorials/building_good_agents) - Best practices for reliable agents
- [Building Effective Agents - Anthropic](https://www.anthropic.com/research/building-effective-agents) - Agent design principles
- [Sharing runs with OpenTelemetry](https://huggingface.co/docs/smolagents/tutorials/inspect_runs) - Details about how to setup OpenTelemetry for tracking your agents.




## Resources

- [smolagents Blog](https://huggingface.co/blog/smolagents) - Introduction to smolagents and code interactions

