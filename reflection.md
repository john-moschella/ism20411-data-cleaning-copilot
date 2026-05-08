  The functions that came primarily from GitHub Copilot’s suggestions were load_data, clean_column_names, and remove_invalid_rows.
I prompted Copilot by first writing comments that explained what I wanted each function to accomplish. For example, before creating 
the column cleaning function, I wrote a comment explaining that the function should standardize column names by removing extra spaces, 
converting them to lowercase, and replacing spaces with underscores. After typing the function name and part of the code structure, 
Copilot generated suggestions using pandas methods. I also used comments before the invalid row function to guide Copilot toward filtering 
out negative prices and quantities. 
  Although Copilot generated a strong starting point, I still needed to modify several parts of the code to better fit the assignment and
my dataset. I simplified some of the variable names and added additional comments to make the code easier to read. I also adjusted the 
logic for handling missing values by filling missing quantities with 0 while dropping rows with missing prices. Another important change 
was adding checks to confirm that columns existed before cleaning them. This was necessary because the raw dataset had inconsistent 
formatting and messy column names, and I wanted to avoid runtime errors if a column name changed unexpectedly.
  Through this project, I learned that data cleaning is an important step before analyzing data because messy datasets can contain 
inconsistent formatting, missing values, and invalid entries that affect results. Using pandas helped me understand how to clean datasets 
efficiently with functions like dropna(), fillna(), string methods, and filtering conditions. One specific example was converting the price
and qty columns to numeric values using pd.to_numeric() with errors="coerce" so invalid values could be handled properly. This made the 
dataset more reliable for future analysis. 
  I also learned that GitHub Copilot is useful for speeding up repetitive coding tasks and providing ideas for functions, but it still 
requires human review and understanding. Some of the suggestions were more complicated than necessary, and a few did not fully match the 
structure of my dataset. For example, Copilot initially assumed cleaner column names than the dataset actually contained, so I had to
modify the code after testing it. This project showed me that Copilot works best as a support tool rather than a replacement for 
problem-solving and debugging skills.
