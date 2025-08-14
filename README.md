# Basic Sales Summary (SQLite + Python)

## Tools & Libraries
- Python 3
- SQLite 
- Pandas
- Matplotlib

## Steps Performed
- Created a small sample dataset in Python.
- Saved the dataset into a SQLite database (`sales_data.db`) in a table named `sales`.
- Ran SQL queries inside Python using `pandas.read_sql_query()`
  
### Query:Total quantity and revenue by product  
```sql
query_product = """
select
  product,
  sum(quantity) AS total_qty,
  sum(quantity * price) AS revenue
from sales
group by product
order by revenue desc;
"""
df_product = pd.read_sql_query(query_product, conn)
df_product 
```
### Outcome

![Outcome](https://github.com/jananiii18/Basic-Sales-Summary/blob/d6cdc3aa55a374b591ddf8736816947387ce6491/Table.png)

### Created bar charts with matplotlib:

```python
plt.figure()
colors = []
max_rev = df_product["revenue"].max()
min_rev = df_product["revenue"].min()

for rev in df_product["revenue"]:
    if rev == max_rev:
        colors.append("green")
    elif rev == min_rev:
        colors.append("red")
    else:
        colors.append("blue")

plt.bar(df_product["product"], df_product["revenue"], color=colors)
plt.title("Revenue by Product Category")
plt.xlabel("Product Category")
plt.ylabel("Revenue")
plt.tight_layout()
plt.show()
```

### Outcome Revenue by Product (highest = green, lowest = red)
![Outcome](https://github.com/jananiii18/Basic-Sales-Summary/blob/38aed362f2e3af059da1ea6433a3f617424093a2/Chart.png)
