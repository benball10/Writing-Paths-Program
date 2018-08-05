# Program that returns the path of each segment

import numpy as np
import pandas as pd

# Reading in table from Excel
# Excel table must have column titles (Ex: Level 1, Level 2, etc.)
df = pd.read_excel(r"C:\Users\Benjamin Ball\Documents\Datonics_Python_Example.xlsx", index_col = None)

# Storing row and column lengths
row_count = df.shape[0]
col_count = df.shape[1]

# Adding new column of length row_count
new_array = np.array(["Test", "Test"], np.dtype(('U', 500)))
new_array.resize(row_count, 1)

# Looping through entire table
i = 0
while i < row_count:
    j = 0
    while j < col_count:
        # Checking for first null value in the row
        if df.isnull().iloc[i][j] == True:
            new_array[i] = str(df.iloc[i][0])
            a = 1
            while a < j:
                new_array[i] = str(new_array[i]).replace("]", "").replace("[", "").replace("'", "") + " - " + str(df.iloc[i][a])
                a += 1
            break
        j += 1

        b = 1
        new_array[i] = df.iloc[i][0]
        while b < j:
            new_array[i] = str(new_array[i]).replace("]", "").replace("[", "").replace("'", "") + " - " + str(df.iloc[i][b])
            b += 1
    i += 1

# Adding the column of paths to the end of the original table
df['Path of Segment'] = new_array

# Writing table to new Excel file
df.to_excel(r"C:\Users\Benjamin Ball\Documents\Datonics_Python_Example2.xlsx", sheet_name = "sheet1", index = False)
