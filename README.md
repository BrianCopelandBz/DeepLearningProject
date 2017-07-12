# Insta Cart Competition

Slowly attempting to get a decent result. Data is stored in /data, but most notebooks manipulate it using sqlite3 in instacart.db in the root folder. 

# Load_sqlite3.ipynb

Grabs the .csv data files and loads into instacart.db. whoa. 

# F1 Score 

Implements f1(pred, actual), a function that takes two dictionaries of {order_id: {product_id, ...}, ...}, where order_id is an integer and product_id is a string, possibly "None".

Other notebooks can insert the following and call f1 to their heart's content. 

```
%run F1_Score.ipynb 
```


# Track Results 

Creates a table called ''model_results'' that will hold the scores of different models along the way. 

No need to call more than once, but you can insert new model results with: 

```
# Open connection to instacart.db
import sqlite3
con = sqlite3.connect("instacart.db")
cur = con.cursor()

# Insert into model results 
cur.execute("INSERT INTO model_results (Model, F1, True_Positives, "
            "False_Positives, False_Negatives) VALUES (?, ?, ?, ?, ?);", 
            list(("Model Name",) + f1(pred,actual) )

# Print contents of model_results
print(pd.read_sql_query("SELECT * FROM model_Results;", con))

con.commit()
con.close()
```
