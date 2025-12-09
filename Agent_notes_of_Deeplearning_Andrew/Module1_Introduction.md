# Module 1 — Introduction to Agentic AI

---

## 1. What is Agentic AI Workflow

An agentic AI workflow is a process where an LLM-based app executes multiple steps to complete a task.  

**Example: Essay Writing Workflow**
- Write an essay outline on a topic  
- Decide whether web research is needed  
- Write a first draft  
- Identify which parts need review  
- Download the essay and feed it to the LLM  
- Human review (if needed)  
- Revise the draft  

---

## 2. Degree of Autonomy

<p align="center">
  <img src="./AG_images/module1/degree_of_autonomy.png" alt="degree of autonomy" width="600"/>
</p>

| Degree                | Characteristics                                                                         |
| --------------------- | --------------------------------------------------------------------------------------- |
| **Less autonomous**   | All steps predetermined;<br>All tool use hard-coded;<br>Autonomy is in text generation. |
| **Semi-autonomous**   | Agent can make some decisions and choose tools;<br>All tools predefined.                |
| **Highly autonomous** | Agent makes many decisions autonomously;<br>Can create new tools on the fly.<br><sub>*(Note: also less controllable and predictable)*</sub> |

---

## 3. Benefits of Agentic Workflow

- Run multiple tasks concurrently for time efficiency  
- Achieve better overall performance  
- Modular structure — easily add, update, or swap tools and models  

---

## 4. What Tasks Are / Aren’t Suited for Agentic AI

**Best suited for:**
- Clear, step-by-step processes  
- Text-based tasks  
- Standardized or procedural workflows  

**Not suitable for:**
- Tasks with unknown steps ahead of time  
- Open-ended planning or problem-solving  
- Multimodal inputs (sound, video, image) that are less predictable  

---

## 5. Task Decomposition

**Steps to design an Agentic Workflow:**
1. Break the task into sequential steps  
2. Determine which steps can be handled by models or tools  
3. If unclear, think how a human would solve the task  
4. Decompose complex tasks into smaller subtasks solvable with the agentic workflow  

| Building Block | Examples              | Use Cases                                                     |
| --------------- | --------------------- | ------------------------------------------------------------- |
| Models          | LLMs                  | Text generation, tool use, information extraction              |
| Models          | Other AI models       | PDF-to-text, text-to-speech, image analysis                    |
| Tools           | API                   | Web search, real-time data, send email, check calendar         |
| Tools           | Information retrieval | Databases, Retrieval-Augmented Generation (RAG)                |
| Tools           | Code execution        | Basic calculation, data analysis                               |

---

## 6. Evaluating Agentic AI

1. Look for low-quality or inconsistent outputs  
2. Add evaluation to track errors (e.g., write code to detect recurring issues, or use another LLM as a judge)  
   - Two types of evaluation: **End-to-End** and **Component-level**

---

## 7. Agentic Design Pattern

### 1. Reflection
Reflection allows an agent to review and evaluate its own past actions or outputs.  
This helps improve reasoning quality and reduce repeated mistakes in multi-step workflows.  

<p align="center">
  <img src="./AG_images/module1/Reflection.png" alt="Reflection" width="500"/>
</p>

---

### 2. Tool Use
Tool use enables the agent to call external APIs or functions to extend its capabilities beyond text generation.  
It bridges reasoning with action — allowing the agent to fetch data, perform computations, or trigger workflows.  

---

### 3. Planning
Planning lets the agent autonomously decide the order and structure of its subtasks.  
This gives more flexibility but reduces control, as the agent dynamically adjusts its plan during execution.  

<p align="center">
  <img src="./AG_images/module1/Planning.png" alt="Planning" width="500"/>
</p>

---

### 4. Multi-Agent Collaboration
Multi-agent collaboration involves multiple specialized agents communicating and coordinating to achieve a shared goal.  
This often leads to better performance through division of labor and collective reasoning.  
