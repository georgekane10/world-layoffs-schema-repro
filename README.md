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

####
