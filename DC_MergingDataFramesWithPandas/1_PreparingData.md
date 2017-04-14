### Import pandas
'''
import pandas as pd
'''

### Read a data file into a DataFrame
Sample Data : list of Olympic medals awarded between 1896 & 2008
bronze = pd.read_csv("Bronze.csv")
silver = pd.read_csv("Silver.csv")
gold = pd.read_csv("Gold.csv")

### Print the first five rows of gold
print(gold.head())
script.py> output:
       NOC         Country   Total
    0  USA   United States  2088.0
    1  URS    Soviet Union   838.0
    2  GBR  United Kingdom   498.0
    3  FRA          France   378.0
    4  GER         Germany   407.0
