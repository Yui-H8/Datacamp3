# Python_AI Agents with Hugging Face smolagents2
---
### Just Add @tool: Writing a Custom Tool

You've just started working at a AgentsCafé, where customers at each table can place multiple drink orders.

Baristas currently hand-write order codes like T5_Latte_20250812_0915, but typos and inconsistent formatting often lead to mix-ups and wrong deliveries.

To fix this, you'll build a simple tool called generate_order_id that takes a table ID, drink name, and appends a timestamp, ensuring every order code is clear and consistent.

Note: The datetime library has been already imported.
* Import the tool decorator from the smolagents library.
* Use the @tool decorator to register your generate_order_id function as a tool.
* Return the formatted order ID string that combines the table ID, drink name, and current timestamp.
```
Add @tool directly above your function to register it.
Return the order_id string.
```
```python
# Import the tool decorator
from smolagents import tool

# Create a tool with the @tool decorator
@tool
def generate_order_id(table_id: str, drink_name: str) -> str:
    """
    Generates a unique order ID for a café order.
    
    Args:
        table_id: The table's identifier (e.g. "T5")
        drink_name: Name of the drink (e.g. "Latte")
    
    Returns:
        A string in the format "{table_id}_{drink_name}_{YYYYMMDD_HHMM}"
    """
    timestamp = datetime.now().strftime("%Y%m%d_%H%M")
    order_id = f"{table_id}_{drink_name}_{timestamp}"
    
    # Return the order ID
    return order_id
```
*Perfect! Being able to define your own custom tools makes the capabilities of AI agents virtually limitless!*

### Check, Please! Giving Agents Access to Data
At AgentsCafé, all drink orders are saved in a file called orders.csv, which includes the columns: table_id, drink_name, and size.

Instead of manually scrolling through the file every time a customer asks for their bill, you’ll build a tool that looks up all current orders for a specific table.

Note: tool and pandas have been imported for you.
* Use table_id as the function parameter so the agent knows which table's orders to retrieve.
* Read the orders.csv file, which contains all drink orders.
* Return the list of drink orders for the table.
```python
# Create a tool that receives the table_id as input
@tool
def lookup_orders(table_id: str) -> list[str]:
    """
    Retrieves the current drink orders for a café table.

    Args:
        table_id (str): The table's identifier (e.g., "T5").

    Returns:
        list[str]: A list of drink orders, each formatted like "Latte (Large)".
    """
    
    # Read the orders.csv file
    df = pd.read_csv('orders.csv')
    orders = df[df['table_id'] == table_id].apply(lambda row: f"{row['drink_name']} ({row['size']})", axis=1).tolist()
    
    # Return the table orders
    return orders
```
*Great job! Being able to provide agents with source-of-truth information essentially allows you to have a conversation with your database, API, or local file.*

### Create a code agent with the lookup_orders and generate_order_id tools
You've already created two tools for AgentsCafé:

* generate_order_id: produces a timestamped ID like T5_Latte_20250812_0915
* lookup_orders: reads orders.csv and returns a list of drinks for that table
  
Now let's create an agent that uses those two tools. So, for any table, the agent can fetch its orders and assign a unique ID to each drink.

Note: The model, tools and necessary imports have already been defined for you. A sample orders.csv is uploaded as well.
* Create a coding agent using your previously defined lookup_orders and generate_order_id tools.
* Add pandas to the list of authorized imports to ensure the agent can read the CSV.
* Use the agent's .run() method to process a task that fetches orders for a table and assigns IDs.
```
Hint
Use the tool names exactly as they appear in the code — both were defined earlier using the @tool decorator.
The tool that looks up orders reads a CSV using pandas, so it must be explicitly authorized.
To run the agent, use the .run(...) method and pass the task string as its argument.
```
```python
# Create a code agent with the lookup_orders and generate_order_id tools
agent = CodeAgent(
    tools=[lookup_orders, generate_order_id],
    model=model,
    # Authorize pandas import
    additional_authorized_imports=['pandas']
)

task = (
    "For table 5, list their current drink orders and generate a unique order ID for each one."
)

# Run the agent passing the task
result = agent.run(task)
print(result)
```
```
print(result)
╭────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── New run ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                                                                                                                                                                                                                                                                                                                              │
│ For table 5, list their current drink orders and generate a unique order ID for each one.                                                                                                                                                                                                                                                                                                                    │
│                                                                                                                                                                                                                                                                                                                                                                                                              │
╰─ LiteLLMModel - openai/gpt-4o-mini ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 1 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  table_id = "T5"                                                                                                                                                                                                                                                                                                                                                                                               
  orders = lookup_orders(table_id)                                                                                                                                                                                                                                                                                                                                                                              
  print("Current drink orders for table 5:", orders)                                                                                                                                                                                                                                                                                                                                                            
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Execution logs:
Current drink orders for table 5: ['Latte (Large)', 'Espresso (Single)', 'Matcha Latte (Small)', 'Flat White (Regular)']

Out: None
[Step 1: Duration 2.46 seconds| Input tokens: 2,018 | Output tokens: 80]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 2 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  order_ids = {}                                                                                                                                                                                                                                                                                                                                                                                                
  for drink in orders:                                                                                                                                                                                                                                                                                                                                                                                          
      order_id = generate_order_id(table_id=table_id, drink_name=drink)                                                                                                                                                                                                                                                                                                                                         
      order_ids[drink] = order_id                                                                                                                                                                                                                                                                                                                                                                               
                                                                                                                                                                                                                                                                                                                                                                                                                
  print("Unique order IDs for each drink:", order_ids)                                                                                                                                                                                                                                                                                                                                                          
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Execution logs:
Unique order IDs for each drink: {'Latte (Large)': 'T5_Latte (Large)_20260113_1641', 'Espresso (Single)': 'T5_Espresso (Single)_20260113_1641', 'Matcha Latte (Small)': 'T5_Matcha Latte (Small)_20260113_1641', 'Flat White (Regular)': 'T5_Flat White (Regular)_20260113_1641'}

Out: None
[Step 2: Duration 3.82 seconds| Input tokens: 4,233 | Output tokens: 190]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ Step 3 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ─ Executing parsed code: ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
  final_answer(order_ids)                                                                                                                                                                                                                                                                                                                                                                                       
 ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 
Final answer: {'Latte (Large)': 'T5_Latte (Large)_20260113_1641', 'Espresso (Single)': 'T5_Espresso (Single)_20260113_1641', 'Matcha Latte (Small)': 'T5_Matcha Latte (Small)_20260113_1641', 'Flat White (Regular)': 'T5_Flat White (Regular)_20260113_1641'}
[Step 3: Duration 4.01 seconds| Input tokens: 6,762 | Output tokens: 333]
{'Latte (Large)': 'T5_Latte (Large)_20260113_1641', 'Espresso (Single)': 'T5_Espresso (Single)_20260113_1641', 'Matcha Latte (Small)': 'T5_Matcha Latte (Small)_20260113_1641', 'Flat White (Regular)': 'T5_Flat White (Regular)_20260113_1641'}
```
*Nicely done! You created a multi-tool agent, authorized pandas for safe execution, and ran it on your task. In Chapter 2, we'll learn how to combine two core AI design patterns: agents and RAG!*
