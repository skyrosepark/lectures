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
# Print top 5 rows of 1st DataFrame in dataframes
print(dataframes[0].head())
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

### Sorting DataFrame with the Index & columns
```
# Read 'monthly_max_temp.csv' into a DataFrame: weather1
weather1 = pd.read_csv('monthly_max_temp.csv', index_col='Month')

# Print the head of weather1
print(weather1.head())

# Sort the index of weather1 in alphabetical order: weather2
weather2 = weather1.sort_index()

# Print the head of weather2
print(weather2.head())

# Sort the index of weather1 in reverse alphabetical order: weather3
weather3 = weather1.sort_index(ascending=False)

# Print the head of weather3
print(weather3.head())

# Sort the index of weather1 numerically using the values of 'Max TemperatureF': weather4
weather4 = weather1.sort_values("Max TemperatureF")

# Print the head of weather4
print(weather4.head())

output:
           Max TemperatureF
    Month                  
    Jan                  68
    Feb                  60
    Mar                  68
    Apr                  84
    May                  88
           Max TemperatureF
    Month                  
    Apr                  84
    Aug                  86
    Dec                  68
    Feb                  60
    Jan                  68
           Max TemperatureF
    Month                  
    Sep                  90
    Oct                  84
    Nov                  72
    May                  88
    Mar                  68
           Max TemperatureF
    Month                  
    Feb                  60
    Jan                  68
    Mar                  68
    Dec                  68
    Nov                  72
```

### Reindexing DataFrame from a list
```

```
