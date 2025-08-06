# 584. Find Customer Referee

## Table: Customer

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

- **id** is the primary key column for this table.  
- Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.  

---

## Problem

Find the names of the customers that are **either**:

1. Referred by any customer with `id != 2`, **or**  
2. Not referred by any customer (i.e., `referee_id` is `NULL`).

Return the result table in **any order**.

---

## Example 1

**Input:**

Customer table:

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

**Output:**

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

---

## Python Solution

```python
import pandas as pd

def find_customer_referee(customer: pd.DataFrame) -> pd.DataFrame:
    # Filter rows where referee_id is NULL or not equal to 2
    result_customer = customer[(customer["referee_id"].isnull()) | (customer["referee_id"] != 2)]
    # Return only the "name" column
    return result_customer[["name"]]


# Example DataFrame
customer = pd.DataFrame([
    [1, "Will", None],
    [2, "Jane", None],
    [3, "Alex", 2],
    [4, "Bill", None],
    [5, "Zack", 1],
    [6, "Mark", 2]
], columns=["id", "name", "referee_id"])

# Run the function
print(find_customer_referee(customer))
``
