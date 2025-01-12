[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/KubaOfca/Blog/tree/main)


# SQL-like Window Functions in Pandas

## What Are Window Functions?
Window functions perform aggregations or calculations across specific partitions of data. Unlike standard aggregation functions, they preserve the table's shape and return a vector of results instead of a single scalar value.

**Documentation (with detailed explanation):** [SQLite Window Functions](https://www.sqlite.org/windowfunctions.html#:~:text=A%20window%20function%20is%20an,it%20is%20a%20window%20function.)

## Use Cases
- Creating new features
- Calculating percentages or rankings

---

## SQL Syntax

### Components
1. **Aggregation Function/Calculation**: Applied to the target column (e.g., `SUM()`, `RANK()`).
2. **`OVER()` Keyword**: Initiates the window function.
3. **`PARTITION BY` Keyword**: Defines the group(s) to apply the function to.
4. **(Optional)** `ORDER BY`: Defines the row order within each partition.

### Example
```sql
SELECT
    DATE(Date) AS Date,
    ticker,
    closing_price,
    MAX(closing_price) OVER(PARTITION BY ticker) AS max_price
FROM
    prices;
```

### Resulting Table
| Date       | ticker | closing_price | max_price |
|------------|--------|---------------|-----------|
| 2023-01-01 | AAPL   | 150           | 155       |
| 2023-01-02 | AAPL   | 155           | 155       |
| 2023-01-03 | GOOG   | 180           | 180       |

---

## Pandas Equivalent

Pandas does not have a dedicated SQL-like syntax for window functions. Instead, it typically uses a combination of `groupby()` and `transform()`.

### Key Functions
- **`groupby()`**: Equivalent to `PARTITION BY` in SQL; defines groups for aggregation.
- **`transform()`**: Applies a function and returns a DataFrame with the same shape as the original. It accepts a lambda or string as input. For functions that already return a vector, `transform()` is not necessary.

### Example

binder link

## Resources
- [SQL-like Window Functions in Pandas](https://engineeringfordatascience.com/posts/sql_like_window_functions_in_pandas/)

