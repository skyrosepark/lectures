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
In this exercise, you'll reindex a DataFrame of quarterly-sampled mean temperature values to contain monthly samples (this is an example of upsampling or increasing the rate of samples, which you may recall from the pandas Foundations course).

The original data has the first month's abbreviation of the quarter (three-month interval) on the Index, namely Apr, Jan, Jul, and Sep. This data has been loaded into a DataFrame called weather1 and has been printed in its entirety in the IPython Shell. Notice it has only four rows (corresponding to the first month of each quarter) and that the rows are not sorted chronologically.
````
print(weather1)
output:
Month          Mean TemperatureF         
Apr            61.956044
Jan            32.133333
Jul            68.934783
Oct            43.434783
````

You'll initially use a list of all twelve month abbreviations and subsequently apply the .ffill() method to forward-fill the null entries when upsampling. This list of month abbreviations has been pre-loaded as year.

```
# Reindex weather1 using the list year: weather2
weather2 = weather1.reindex(year)

# Print weather2
print(weather2)

# Reindex weather1 using the list year with forward-fill: weather3
weather3 = weather1.reindex(year).ffill()

# Print weather3
print(weather3)

output:
           Mean TemperatureF
    Month                   
    Jan            32.133333
    Feb                  NaN
    Mar                  NaN
    Apr            61.956044
    May                  NaN
    Jun                  NaN
    Jul            68.934783
    Aug                  NaN
    Sep                  NaN
    Oct            43.434783
    Nov                  NaN
    Dec                  NaN
           Mean TemperatureF
    Month                   
    Jan            32.133333
    Feb            32.133333
    Mar            32.133333
    Apr            61.956044
    May            61.956044
    Jun            61.956044
    Jul            68.934783
    Aug            68.934783
    Sep            68.934783
    Oct            43.434783
    Nov            43.434783
    Dec            43.434783
```

### Reindexing using another DataFrame Index
```
# Shape of names_1981 DataFrame: (19455, 1)
# Shape of names_1881 DataFrame: (1935, 1)

names_1981 = pd.read_csv('names1981.csv', header=None, names=['name', 'gender', 'count'], index_col=(0,1))
names_1881 = pd.read_csv('names1881.csv', header=None, names=['name', 'gender', 'count'], index_col=(0,1))

# Reindex names_1981 with index of names_1881: common_names
common_names = names_1981.reindex(names_1881.index)

# Print shape of common_names
print(common_names.shape)

# Drop rows with null counts: common_names
common_names = common_names.dropna()

# Print shape of new common_names
print(common_names.shape)

Shape of names_1981 DataFrame: (19455, 1)
Shape of names_1881 DataFrame: (1935, 1)
```

### Broadcasting in arithmetic formulas
```
# data from wunderground.com
# Extract selected columns from weather as new DataFrame: temps_f
temps_f = weather[['Min TemperatureF','Mean TemperatureF','Max TemperatureF']]

# Convert temps_f to celsius: temps_c
temps_c = (temps_f - 32) * 5/9

# Rename 'F' in column names with 'C': temps_c.columns
temps_c.columns = temps_c.columns.str.replace('F', 'C')

# Print first 5 rows of temps_c
print(temps_c.head())

output:
                Min TemperatureC  Mean TemperatureC  Max TemperatureC
    Date                                                             
    2013-01-01         -6.111111          -2.222222          0.000000
    2013-01-02         -8.333333          -6.111111         -3.888889
    2013-01-03         -8.888889          -4.444444          0.000000
    2013-01-04         -2.777778          -2.222222         -1.111111
    2013-01-05         -3.888889          -1.111111          1.111111

```

### Computing percentage growth of GDP
```
# data from Federal Reserve Bank of St.Louis

# Read 'GDP.csv' into a DataFrame: gdp
gdp = pd.read_csv('GDP.csv', index_col='DATE', parse_dates=True)

# Slice all the gdp data from 2008 onward: post2008
post2008 = gdp['2008':]

# Print the last 8 rows of post2008
print(post2008.tail(8))

# Resample post2008 by year, keeping last(): yearly
yearly = post2008.resample('A').last()

# Print yearly
print(yearly)

# Compute percentage growth of yearly: yearly['growth']
yearly['growth'] = yearly.pct_change() * 100

# Print yearly again
print(yearly)

output:
                  VALUE
    DATE               
    2014-07-01  17569.4
    2014-10-01  17692.2
    2015-01-01  17783.6
    2015-04-01  17998.3
    2015-07-01  18141.9
    2015-10-01  18222.8
    2016-01-01  18281.6
    2016-04-01  18436.5
                  VALUE
    DATE               
    2008-12-31  14549.9
    2009-12-31  14566.5
    2010-12-31  15230.2
    2011-12-31  15785.3
    2012-12-31  16297.3
    2013-12-31  16999.9
    2014-12-31  17692.2
    2015-12-31  18222.8
    2016-12-31  18436.5
                  VALUE    growth
    DATE                         
    2008-12-31  14549.9       NaN
    2009-12-31  14566.5  0.114090
    2010-12-31  15230.2  4.556345
    2011-12-31  15785.3  3.644732
    2012-12-31  16297.3  3.243524
    2013-12-31  16999.9  4.311144
    2014-12-31  17692.2  4.072377
    2015-12-31  18222.8  2.999062
    2016-12-31  18436.5  1.172707
```
