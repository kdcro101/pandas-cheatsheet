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
df.loc[0,'name'] = 123
```

### Querying DataFrame
```py
# get all where 'val' > 55.00
df.loc[df['val'] > 55.00]
# get nth where 'val' > 55.00 - returns row only not array of length=1
df.loc[df['val'] > 55.00].iloc[0]

# get top 1 row - returns array of rows of length=1
df.loc[df['val'] > 55.00].head(1)
# get top n rows - returns array of rows
df.loc[df['val'] > 55.00].head(5)
```
### TorchText.Dataset from Pandas DataFrame
```py

TEXT = data.Field(tokenize='spacy')
# example with lambda across LABEL values
LABEL = data.LabelField(preprocessing=data.Pipeline(lambda x: pro_proc(x)))
FIELDS = {'title': ('text', TEXT), 'change_prc': ('label', LABEL)}

def create_dataset(dataframe,text_column,label_column, TEXT_FIELD, LABEL_FIELD):
    # idData pair training is useless during training, use None to specify its corresponding field
    fields = [(text_column, TEXT_FIELD), (label_column, LABEL_FIELD)]       
    examples = []
 
    for text, label in tqdm(zip(dataframe[text_column], dataframe[label_column])):
        examples.append(data.Example.fromlist([text, label], fields))
 
    return examples, fields

# use as
train_examples, train_fields = create_dataset(dataFrame,"title","change_prc", TEXT, LABEL)

train = data.Dataset(train_examples, FIELDS)

```
