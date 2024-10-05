# Filtering, Ordering, and Limiting Data with SQL - Lab


## Introduction
In this lab, you will practice writing SQL `SELECT` queries that limit results based on conditions, using `WHERE`, `ORDER BY`, and `LIMIT`.

## Objectives
You will practice the following:

* Order the results of your queries by using `ORDER BY` (`ASC` & `DESC`)
* Limit the number of records returned by a query using `LIMIT`
* Write SQL queries to filter and order results

## The Data

Here's a database full of famous dogs!  The `dogs` table is populated with the following data:

|name      |age    |gender |breed           |temperament|hungry |
|----------|-------|-------|----------------|-----------|-------|
|Snoopy    |3      |M      |beagle          |friendly   |1      |
|McGruff   |10     |M      |bloodhound      |aware      |0      |
|Scooby    |6      |M      |great dane      |hungry     |1      |
|Little Ann|5      |F      |coonhound       |loyal      |0      |
|Pickles   |13     |F      |black lab       |mischievous|1      |
|Clifford  |4      |M      |big red         |smiley     |1      |
|Lassie    |7      |F      |collie          |loving     |1      |
|Snowy     |8      |F      |fox terrier     |adventurous|0      |
|NULL      |4      |M      |golden retriever|playful    |1      |

## Connecting to the Database

In the cell below, import `pandas` and `sqlite3`. Then establish a connection to the database `dogs.db`.

Look at all of the data in the table by selecting all columns from the `dogs` table with `pd.read_sql`.


```python
import sqlite3
import pandas as pd
conn = sqlite3.connect('dogs.db')
```

 

## Queries

Display the outputs for each of the following query descriptions.

### Select the name and breed for all female dogs

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>WHERE</code> with the <code>=</code> operator</p>
</details>


```python
pd.read_sql("""
SELECT name, breed
FROM dogs
WHERE gender = 'F'
""",conn)
```

### Select the number of dogs that do not have a name

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>COUNT</code> and <code>IS NULL</code></p>
</details>


```python
pd.read_sql("""
SELECT COUNT(*) AS num_of_dogs_without_name
FROM dogs
WHERE name IS NULL
""", conn)
```

### Select the names of all dogs that contain the double letters `ff` or `oo`

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>LIKE</code>, <code>%</code>, and <code>OR</code></p>
</details>


```python
pd.read_sql ("""
SELECT name
FROM dogs
WHERE name LIKE '%ff%' OR name LIKE '%oo%'
""", conn)
```

### Select the names of all dogs listed in alphabetical order.  Notice that SQL lists the nameless dog first.

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>ORDER BY</code></p>
</details>


```python
pd.read_sql("""
SELECT name
FROM dogs
ORDER BY name
""", conn)
```

### Select the name and breed of only the hungry dogs and list them from youngest to oldest


```python
pd.read_sql("""
SELECT name, breed
FROM dogs
WHERE hungry = 1
ORDER BY age ASC
""", conn)
```

### Select the oldest dog's name, age, and temperament

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>ORDER BY</code> with <code>LIMIT</code></p>
</details>


```python
pd.read_sql("""
SELECT name, age, temperament
FROM dogs
ORDER BY age DESC
LIMIT 1
""", conn)
```

### Select the name and age of the three youngest dogs


```python
pd.read_sql("""
SELECT name, age
FROM dogs
ORDER BY age ASC
LIMIT 3
""", conn)
```

### Select the name and breed of the dogs who are between five and ten years old, ordered from oldest to youngest

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>WHERE</code> with <code>BETWEEN</code></p>
</details>


```python
pd.read_sql("""
SELECT name, breed
FROM dogs
WHERE age BETWEEN 5 AND 10
ORDER BY age DESC
""", conn)
```

### Select the name, age, and hungry columns for hungry dogs between the ages of two and seven.  This query should also list these dogs in alphabetical order.


```python
pd.read_sql("""
SELECT name, age, hungry
FROM dogs
WHERE hungry = 1 AND age BETWEEN 2 AND 7
ORDER BY name
""", conn)
```

## Close the Database Connection


```python
conn.close()
```

## Summary

Great work! In this lab you practiced writing more complex SQL statements to not only query specific information but also define the quantity and order of your results. 
