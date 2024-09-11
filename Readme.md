
# Data Analytics with Python and SQL

## Table of Contents
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Technologies Used](#technologies-used)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Example Queries](#example-queries)
7. [Data Visualization](#data-visualization)
8. [License](#license)

## Project Overview
This project demonstrates how to use Python and SQL to perform data analytics on a relational database. It covers connecting to a MySQL database, executing SQL queries to extract useful insights, and visualizing the results using Python libraries like Pandas, Matplotlib, and Seaborn.

The project showcases how SQL is used for querying and managing the database, while Python handles data manipulation and visualization.

## Features
- Connect to MySQL databases using `mysql-connector`.
- Perform complex SQL queries to extract insights from large datasets.
- Use Python to clean and transform the data for analysis.
- Visualize results with popular Python libraries like Matplotlib and Seaborn.
- Examples of running analytical queries (e.g., `JOIN`, `GROUP BY`, `DISTINCT`).
- Export data results into CSV files for reporting.

## Technologies Used
- **Python**: Version 3.x
  - Pandas
  - Matplotlib
  - Seaborn
  - MySQL-connector
- **SQL**: MySQL for data querying.
- **MySQL**: As the database management system.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/data-analytics-python-sql.git
   cd data-analytics-python-sql
   ```

2. **Install Python dependencies**:
   Install the required libraries using `pip`:

   ```bash
   pip install mysql-connector-python pandas matplotlib seaborn
   ```

3. **Set up MySQL Database**:
   - Install MySQL and set up your local database or connect to an existing database.
   - Create the necessary tables and insert data into them, or import sample data (e.g., `customers`, `sales`, etc.).

## Usage

1. **Connect to the Database**:
   Update the database credentials in your Python script:

   ```python
   db = mysql.connector.connect(
       host="127.0.0.1",      # or "localhost"
       port=3306,             # MySQL port, default is 3306
       user="root",           # Your MySQL username
       password="your_password",  # Your MySQL password
       database="ecommerce"   # Database name
   )
   ```

2. **Run SQL Queries**:
   Example SQL queries to extract and analyze data:

   ```python
   # Extract distinct customer cities
   cur.execute("SELECT DISTINCT customer_city FROM customers")
   cities = cur.fetchall()
   ```

3. **Data Visualization**:
   Use `Pandas` and `Matplotlib` to manipulate and visualize the data:

   ```python
   import pandas as pd
   import matplotlib.pyplot as plt

   df = pd.DataFrame(cities, columns=['Customer City'])
   df['Customer City'].value_counts().plot(kind='bar')
   plt.title("Customer Distribution by City")
   plt.show()
   ```

4. **Export Data**:
   You can export query results to CSV for further analysis:

   ```python
   df.to_csv('customer_cities.csv', index=False)
   ```

## Example Queries

- **Get total sales by product category**:
   ```sql
   SELECT category_name, SUM(sales_amount) AS total_sales
   FROM sales
   JOIN products ON sales.product_id = products.product_id
   GROUP BY category_name;
   ```

- **Find the most popular products**:
   ```sql
   SELECT product_name, COUNT(*) AS times_ordered
   FROM orders
   JOIN products ON orders.product_id = products.product_id
   GROUP BY product_name
   ORDER BY times_ordered DESC;
   ```

- **Customer city analysis**:
   ```python
   cur.execute("SELECT customer_city, COUNT(*) FROM customers GROUP BY customer_city;")
   result = cur.fetchall()
   ```

## Data Visualization

Below are some common visualizations performed using the queried data:

- **Bar Charts**: To visualize categorical data, like sales by category or customer distribution by city.
- **Line Charts**: To track changes over time, such as sales over months.
- **Pie Charts**: To visualize proportions in the data, like market share by product.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Example: Plotting sales by category
df = pd.DataFrame(result, columns=['Category', 'Total Sales'])
sns.barplot(x='Category', y='Total Sales', data=df)
plt.title("Total Sales by Product Category")
plt.xticks(rotation=45)
plt.show()
```
