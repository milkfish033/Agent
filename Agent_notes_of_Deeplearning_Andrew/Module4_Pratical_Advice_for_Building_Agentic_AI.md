# 1. Evaluation

Example: invoice processing workflow

common issue: mix up dates

Solution: crate an eval function to measure date extraction accuracy

### Eval for Date Extraction

1. **Collect Ground Truth, Create Test Cases First**
   - Manually extract due dates from 10–20 invoices.

2. **Set Output Format in Prompt**
   - Example instruction: *"Format the due date as `YYYY/MM/DD`"*.

3. **Extract Model Output Programmatically**
   ```python
   import re
   date_pattern = r'\d{4}/\d{2}/\d{2}'
   extracted_date = re.findall(date_pattern, llm_response)

4. **Compare with Ground Truth**
    ```
    if extracted_date == actual_date:
        num_correct += 1
    ```
5. **Compute Accuracy**

    `accuracy = num_correct / total_invoices`

### Two Axes of Evaluation

|                         | **Evaluate with Code (Objective)** | **LLM-as-Judge (Subjective)** |
|-------------------------|------------------------------------|--------------------------------|
| **Per-example ground truth** | **Invoice date extraction**<br>```python<br>if extracted_date == actual_date:<br>    num_correct += 1<br>``` | **Count gold-standard talking points**<br>*"Count the number of required points mentioned in this text..."* |
| **No per-example ground truth** | **Check marketing copy length**<br>```python<br>if len(text) <= 10:<br>    num_correct += 1<br>``` | **Grade with a rubric**<br>*"Grade this chart based on clarity of axis labels, readability, etc."* |

### Tips for Designing End-to-End Evals

- **Start simple:**  
  Quick and dirty is fine at the beginning — don’t over-engineer your first version.

- **Iterate with human feedback:**  
  When your evals fail to align with human judgment of which system is better, use that as a signal to refine your metric.

- **Benchmark against humans:**  
  Identify areas where model performance is worse than humans and focus improvement there.



# 2. Error Analysis and Prioritizing Next Steps
count up errors in each step in the whole pipeline

### Tips for Error Analysis

- **Inspect traces regularly:**  
  Build a habit of reviewing intermediate outputs to see where things go wrong.

- **Identify failing components:**  
  Use error analysis to determine which part of the pipeline performed poorly and caused the bad result.

- **Focus improvement efforts strategically:**  
  Let error analysis guide where to invest time and resources for the biggest impact.

# 3. Address the Problem You Identify 

### Improving Non-LLM Component Performance

Examples include: web search, RAG retrieval, code execution, speech recognition models, object detection models, etc.

- **Tune hyperparameters of the component**
  - Web search: number of results, date range
  - RAG: similarity threshold, chunk size
  - ML models: detection / confidence threshold

- **Replace the component**
  - Try a different web search engine
  - Swap to a different RAG retriever/provider
  - Use a stronger pre-trained ML model

- **Improve your prompts**
  - Add clearer, more explicit instructions
  - Include one or more concrete examples (few-shot prompting)

- **Try a new model**
  - Evaluate multiple LLMs and choose the best-performing one

- **Split up the step**
  - Break the task into smaller, simpler steps

- **Fine-tune a model**
  - Fine-tune using your internal data to boost performance for your specific use case

- **Improve Prompt**

# 4. Latency, Cost Optimization

- Benchmark execution time for each pipeline step

- Introduce parallelization where possible

- Use smaller / faster models when acceptable

- Balance compute cost vs. accuracy based on business requirements