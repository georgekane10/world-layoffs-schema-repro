# World Layoffs Data Cleaning Project

## Project Overview
This Project involves cleaning a global layoffs dataset using MySQL. 
The Main goal was to transform this raw, messy data into a clean structured format,
so that I could carry out an exploratory analysis of the layoffs dataset.

### Data Staging
To ensure the raw data remained untouched, I created a staging table.
This allowed me to clean, transform, and make necessary changes on a copy of the data 
keeping the original dataset as a secure backup.

#### Removing Duplicates
To identify any duplicates in the data, I used a CTE along with the ROW_NUMBER() function.
I partitioned the data by all of the columns. This assigned a row number for each distinct row.
Now I would be able to identify any duplicates in the data, because any row with a row number greater 
than 1 indicated that this row appeared more than once. Then, I created another staging table, in which I used
the same row number over partitioning all of the columns which I did for the duplicate CTE table. This table now had all the 
data but also an additional row number column. Finally, I deleted any row that had a row number greater than 1.

#### Standardising Data
To standardise the data, the first thing I did was remove any hidden spaces that could cause grouping errors.
I applied the TRIM() function to remove the spaces. Next, I fixed inconsistencies in the data. For example, changing 'cryptocurrency' to just 'crypto'.
I also identified a specific error in the country column where some records for 'United States' had a trailing full stop that would interfere with grouping.
Finally, since the date was as a text data type, we used the STR_TO_DATE() function to change it to a date data type.

#### Removing Nulls or Blanks
In the data there were several nulls in important columns such as industry. I used a query that populated a null or a blank value using existing data 
from the same table. By aliasing layoffs_staging5 as two seperate tables (1 & 2), I joined them on the company and location. Having the WHERE clause where table 1 industry had a blank or null, and table 2 industry was populated, this allowed me to identify rows where the industry was missing and fill them using matching
records where the industry was already populated. Now i was able to update the missing or null industry values with its correct value using existing data from the rest of the dataset.

#### Removing any columns or rows
Finally the last thing I needed to do was remove the row number from layoffs_staging5 we added in to remove duplicates, as it would be unnecessary for the exploratory data analysis.









