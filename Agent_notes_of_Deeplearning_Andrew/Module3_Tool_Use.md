# 1. What are tools

# 2. Creating a tool 
 Prompting an LLM to Use Tools 

Goal:
Enable an LLM to call a tool (e.g., `get_current_time`) when a user asks a question it can’t answer directly.

## System Prompt
> You have access to a tool called **get_current_time**.  
> To use it, return exactly:
>
> ```
> FUNCTION:
> get_current_time()
> ```

## Tool (API)
- **Name:** `get_current_time`
- **Behavior:** returns the current time as a string
- **Example implementation:**
  ```python
  from datetime import datetime

  def get_current_time():
      """Returns the current time as a string"""
      return datetime.now().strftime("%H:%M:%S")

# 3. Tool Syntax

# 4. Code execution

# 5. MCP

MCP is a protocol 