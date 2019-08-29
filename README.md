# Pandas cheatsheet
https://pandas.pydata.org/


### Iterate through DataFrame rows
```py
for index, row in df.iterrows():
     print(index, row)
```

### Histogram for string value count in column
```py
df.label.value_counts().to_frame().style.bar()
```
### Sorting the column
```py
## accending
df.sort_values(by=['Brand'], inplace=True)
## descending 
df.sort_values(by=['Brand'], inplace=True, ascending=False)

```

### Adding column with default value
```py
CRUDE_DATA["new_column"] = None
```

### Updating row
