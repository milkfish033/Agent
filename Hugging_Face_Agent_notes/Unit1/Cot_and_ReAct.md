## 🔗 Chain-of-Thought (CoT)

**Chain-of-Thought (CoT)** is a prompting technique that guides a model to **think through a problem step-by-step before producing a final answer.**

It typically starts with:  
> *"Let's think step by step."*

This approach helps the model **reason internally**, especially for logical or mathematical tasks, **without interacting with external tools**.

### ✅ Example (CoT)
```
Question: What is 15% of 200?
Thought: Let's think step by step. 10% of 200 is 20, and 5% of 200 is 10, so 15% is 30.
Answer: 30
```

## ⚙️ ReAct: Reasoning + Acting

A key method is the **ReAct approach**, which combines "Reasoning" (Think) with "Acting" (Act). 

ReAct is a prompting technique that encourages the model to think step-by-step and interleave actions (like using tools) between reasoning steps.

This enables the agent to solve complex multi-step tasks by alternating between:
- Thought: internal reasoning
- Action: tool usage
- Observation: receiving tool output
### 🔄 Example (ReAct)
```
Thought: I need to find the latest weather in Paris.
Action: Search["weather in Paris"]
Observation: It's 18°C and cloudy.
Thought: Now that I know the weather...
Action: Finish["It's 18°C and cloudy in Paris."]
```

## 🔁 Comparison: ReAct vs. CoT

| Feature              | Chain-of-Thought (CoT)      | ReAct                               |
|----------------------|-----------------------------|-------------------------------------|
| Step-by-step logic   | ✅ Yes                      | ✅ Yes                              |
| External tools       | ❌ No                       | ✅ Yes (Actions + Observations)     |
| Best suited for      | Logic, math, internal tasks | Info-seeking, dynamic multi-step tasks |
