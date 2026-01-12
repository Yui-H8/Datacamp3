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
from smolagents import decorator

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
