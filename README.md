# Program that returns the path of each segment

import numpy as np
import pandas as pd

# Reading in table from Excel
# Must read in table with column titles
df = pd.read_excel(r"C:\Users\Benjamin Ball\Documents\Python_Example.xlsx", index_col = None)
print(df)

# Storing row and column lengths
row_count = df.shape[0]
col_count = df.shape[1]

# Add new column of length row_count
new_array = np.array(["Test", "Test"], np.dtype(('U', 500)))
new_array.resize(row_count, 1)

# Looping through entire table
i = 0
while i < row_count:
    j = 0
    while j < col_count:
        # Checking for first null value in the row
        if df.isnull().iloc[i][j] == True:
            new_array[i] = str(df.iloc[i][0])  # Change from "j + 1" to "j" if not including "Level 1" column in Excel
            a = 1
            while a < j:
                new_array[i] = str(new_array[i]) + " - " + str(df.iloc[i][a])
                a += 1
            break
        j += 1
        #new_array[i] = df.iloc[i][j - 1] ??(this is from names program)
    i += 1

# Adding the column of names to the end of the original table
df['Path of Segment'] = new_array

print(df)

# Writing table to Excel
df.to_excel(r"C:\Users\Benjamin Ball\Documents\Python_Example2.xlsx", sheet_name = "sheet1", index = False)

#bugs: doesn't return highest level into new column (k loop tries to fix this); prints name as "Leve" instead of "Level 2"
