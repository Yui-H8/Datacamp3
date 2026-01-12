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
