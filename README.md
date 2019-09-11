# Pandas cheatsheet
https://pandas.pydata.org/


### Plot multiple series with ma
```py
import matplotlib.pyplot as plt

df = pd.read_csv(csv_filepath)

df.plot(x='epoch', y=["series1", "series2"], figsize=(32, 18), grid=True, color=["red","green"])

plt.savefig(os.path.join(self.ROOT, 'report.pdf'))
plt.savefig(os.path.join(self.ROOT, 'report.png'))
```
### Get columns in DataFrame
```py
list = df.columns
```
### Add column with Moving Average
```py
df["ma"] = df.rolling(window=10)['column'].mean()
# then plot it
df.plot(x="date",y="ma",figsize=(16,9),linewidth=0.5)
```

### Modify limit when printing series
```py
# set new limit
pd.set_option('display.max_rows', 1_000_000)
# reset limit
pd.reset_option('display.max_rows')
```

### Check value in index
```py
10090723 not in self.df.index.values
```

### Iterate through DataFrame rows
```py
for index, row in df.iterrows():
     print(index, row)
```

### Histograms
```py
#string value
df.label.value_counts().to_frame().style.bar()
# numerical
df["column"].hist(figsize=(16,9),bins=50)

```

### Ploting
```py
df.plot(x="date",y="Change")
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

# comparison operators
df.loc[df['val'] > 55.00].head(5)
df.loc[df['val'] == 55.00].head(5)
df.loc[df['val'] != 55.00].head(5)
df.loc[df['val'].isin(['a','b','c'])]

#check for None 
df.loc[df['change2'].isnull()].head(1)
#check for NOT None 
df.loc[~df['change2'].isnull()].head(1)


# logical - combine
df.loc[(df['val'] >= 0) & (df['column_name'] <= 101)]

```
### torchtext.data.Dataset from Pandas DataFrame
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
