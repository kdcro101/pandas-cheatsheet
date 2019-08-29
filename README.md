# Pandas cheatsheet
https://pandas.pydata.org/


### Histogram for string value count in column
```py
DF.label.value_counts().to_frame().style.bar()
```
