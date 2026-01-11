# AI Agents with Hugging Face smolagents
---
**What you'll learn**
Understand how smolagents' code agents work and why they’re powerful

Build agents that solve real-world tasks using Python

Create custom tools to extend what agents can do

Design multi-agent workflows to solve more complex problems

**Description**

AI agents are changing how we work with data and software. From automating workflows to helping users navigate complex tasks, agents can search, reason, and act on your behalf. In this course, you’ll learn how to build agents using smolagents, a lightweight Python framework developed by Hugging Face.

https://campus.datacamp.com/courses/ai-agents-with-hugging-face-smolagents/

---
### Let the Agent Do the Math: Expense Insights
You've been manually tracking your monthly expenses in a spreadsheet, but analyzing spending patterns takes forever.

Your friend recommended trying smolagents to automate the analysis. Your weekly expense data for the past month is given in the following expense_data dictionary:
```
expense_data = {
    "groceries": [120, 95, 110, 140],
    "utilities": [85, 92, 78, 88],
    "entertainment": [45, 0, 75, 30],
    "transportation": [60, 55, 70, 65]
}
```
Let's run an agent that can help you understand your spending habits and create a budget plan.

Note: The agent and expense_data dictionary have been already initialized for you.
* Run the provided code to see smolagents analyze your expense data.
* Observe the output and how the agent writes Python code to find spending patterns.
```python
# Task for the agent
task = f"""Analyze my monthly expense data by category. Calculate total spending per category, find my highest expense area, and suggest a realistic budget for next month. Use simple text format in your final answer. Here is my weekly expense data for the past four weeks:

{expense_data}
"""

# Execute the financial analysis
result = agent.run(task)

print("Personal finance analysis:\n")
print(result)
```
```

╭────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── New run ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                                                                                                                                                                                                                                                                                                                              │
│ Analyze my monthly expense data by category. Calculate total spending per category, find my highest expense area, and suggest a realistic budget for next month. Use simple text format in your final answer. Here is my weekly expense data for the past four weeks:                                                                                                                                        │
│                                                                                                                                                                                                                                                                                                                                                                                                              │
│ {'groceries': [120, 95, 110, 140\], 'utilities': [85, 92, 78, 88\], 'entertainment': [45, 0, 75, 30\], 'transportation': [60, 55, 70, 65\]}                                                                                                                                                                                                                                                                  │
│                                                                                                                                                                                                                                                                                                                                                                                                              │
╰─ LiteLLMModel - openai/gpt-4o-mini ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 1 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  weekly_expenses = {                                                                                                                                                                                                                                                                                                                                                                                           
      'groceries': [120, 95, 110, 140],                                                                                                                                                                                                                                                                                                                                                                         
      'utilities': [85, 92, 78, 88],                                                                                                                                                                                                                                                                                                                                                                            
      'entertainment': [45, 0, 75, 30],                                                                                                                                                                                                                                                                                                                                                                         
      'transportation': [60, 55, 70, 65]                                                                                                                                                                                                                                                                                                                                                                        
  }                                                                                                                                                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                                                                                                                
  total_spending = {category: sum(expenses) for category, expenses in weekly_expenses.items()}                                                                                                                                                                                                                                                                                                                  
  print("Total spending per category:", total_spending)                                                                                                                                                                                                                                                                                                                                                         
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Execution logs:
Total spending per category: {'groceries': 465, 'utilities': 343, 'entertainment': 150, 'transportation': 250}

Out: None
[Step 1: Duration 4.54 seconds| Input tokens: 1,996 | Output tokens: 178]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 2 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  highest_expense_category = max(total_spending, key=total_spending.get)                                                                                                                                                                                                                                                                                                                                        
  highest_expense_value = total_spending[highest_expense_category]                                                                                                                                                                                                                                                                                                                                              
  suggested_budget = highest_expense_value * 1.10  # Increase by 10%                                                                                                                                                                                                                                                                                                                                            
  print(f"Highest expense area: {highest_expense_category} (${highest_expense_value})")                                                                                                                                                                                                                                                                                                                         
  print(f"Suggested budget for next month: ${suggested_budget:.2f}")                                                                                                                                                                                                                                                                                                                                            
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Execution logs:
Highest expense area: groceries ($465)
Suggested budget for next month: $511.50

Out: None
[Step 2: Duration 4.68 seconds| Input tokens: 4,381 | Output tokens: 376]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 3 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  final_answer("Total spending per category:\n"                                                                                                                                                                                                                                                                                                                                                                 
               "- Groceries: $465\n"                                                                                                                                                                                                                                                                                                                                                                            
               "- Utilities: $343\n"                                                                                                                                                                                                                                                                                                                                                                            
               "- Entertainment: $150\n"                                                                                                                                                                                                                                                                                                                                                                        
               "- Transportation: $250\n"                                                                                                                                                                                                                                                                                                                                                                       
               "\n"                                                                                                                                                                                                                                                                                                                                                                                             
               f"Highest expense area: Groceries ($465)\n"                                                                                                                                                                                                                                                                                                                                                      
               f"Suggested budget for next month: $511.50")                                                                                                                                                                                                                                                                                                                                                     
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Final answer: Total spending per category:
- Groceries: $465
- Utilities: $343
- Entertainment: $150
- Transportation: $250

Highest expense area: Groceries ($465)
Suggested budget for next month: $511.50
[Step 3: Duration 3.02 seconds| Input tokens: 7,132 | Output tokens: 514]
Personal finance analysis:

Total spending per category:
- Groceries: $465
- Utilities: $343
- Entertainment: $150
- Transportation: $250

Highest expense area: Groceries ($465)
Suggested budget for next month: $511.50
```
*Great job running your first coding agent! You didn't have to create any tools for your agent here, either; the LLM reasoned and wrote its own code to analyze the data as you requested.*

### Wait, You Didn't Write Any Functions?
After watching an agent analyze your expenses, you're fascinated by how it calculated totals, identified patterns, and created budget recommendations all in one go.

Later, your roommate asks: "How was that possible without you giving it any functions directly?"

You realize it's because the agent wasn't just calling functions; it was writing and running code.

What's the main difference between how a code agent and a function-calling agent would solve a task?
```
Code agents can only work with financial data, while function-calling agents work with any data type
〇 Code agents write scripts to handle calculations, while function-calling agents make separate calls to predefined functions
Code agents use JSON to process numbers more efficiently than function-calling agents
Code agents are always more accurate at calculations than function-calling agents
```
*Exactly! Code agents write code behind the scenes, combining logic, calculations, and analysis into one workflow.*

---
### Writing Code Through Prompts: Compound Interest
You're setting aside a fixed amount of money each month into a savings account that earns interest.

Rather than calculating compound interest manually or in a spreadsheet, you decide to use an agent to write the code for you and answer your queries.

Note: For all exercises in this course, a model variable has already been initialized for you. It provides access to an OpenAI model behind the scenes. No setup or API keys required.
* Import the CodeAgent class from the smolagents library.
* Create an instance of CodeAgent, passing it an empty list for tools.
* Call the .run() method on your agent and pass in your task string.
```
Hint
The class you need to import is called CodeAgent.
Set tools=[] when creating the agent; you're not using any tools yet.
To run the agent, use .run(...) and pass your task as a string.
```
