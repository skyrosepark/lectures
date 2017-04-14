### Reading DataFrames from multiple files
```
# Import pandas
import pandas as pd
```

```
# Read a data file into a DataFrame
# Sample Data : list of Olympic medals awarded between 1896 & 2008
bronze = pd.read_csv("Bronze.csv")
silver = pd.read_csv("Silver.csv")
gold = pd.read_csv("Gold.csv")
```

```
# Print the first five rows of gold
print(gold.head())
output:
       NOC         Country   Total
    0  USA   United States  2088.0
    1  URS    Soviet Union   838.0
    2  GBR  United Kingdom   498.0
    3  FRA          France   378.0
    4  GER         Germany   407.0
```

### Reading DataFrames from multiple files in a loop
```
# Creat the list of file names : filenames
filenames = ['Gold.csv', 'Silver.csv', 'Bronze.csv']
dataframes = []
for filename in filenames:
    dataframes.append(pd.read_csv(filename))
```

### Combining DataFrames from multiple data files
```
# Make a copy of gold: medals
medals = gold.copy()

# Create list of new column labels: new_labels
new_labels = ['NOC', 'Country', 'Gold']

# Rename the columns of medals using new_labels
medals.columns = new_labels

# Add columns 'Silver' & 'Bronze' to medals
medals['Silver'] = silver['Total']
medals['Bronze'] = bronze['Total']

print(medals.head())
output:
       NOC         Country    Gold  Silver  Bronze
    0  USA   United States  2088.0  1195.0  1052.0
    1  URS    Soviet Union   838.0   627.0   584.0
    2  GBR  United Kingdom   498.0   591.0   505.0
    3  FRA          France   378.0   461.0   475.0
    4  GER         Germany   407.0   350.0   454.0
```
