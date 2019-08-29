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
# accending
df.sort_values(by=['Brand'], inplace=True)
# descending 
df.sort_values(by=['Brand'], inplace=True, ascending=False)

```

### Adding column
```py
# with default value
df["new_column"] = None
# with data
df['capital city'] = ['Rome','Madrid','Athens','Paris','Lisbon']

```
### Rename column
```py
dfnew = df.rename(columns={'old_name': 'new_name'})
```
### Removing column
```py
# Delete using del 
del df['column_to_remove']
# Delete using drop() 
df = df.drop(['column_to_remove'], axis=1)
```

### Updating row
```py
# Update column 'name' at index 0
df[0,'name'] = 123
```
