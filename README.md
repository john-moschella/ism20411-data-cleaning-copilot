# ism20411-data-cleaning-copilot
"""
data_cleaning.py

Purpose:
This script cleans a messy sales dataset by:
- standardizing column names
- removing extra whitespace
- handling missing values
- removing invalid rows

The cleaned dataset is saved to the processed folder.
"""

import pandas as pd


# Copilot-assisted function:
# Load the CSV dataset into a pandas DataFrame.
def load_data(file_path: str):
    df = pd.read_csv(file_path)
    return df


# Copilot-assisted function:
# Standardize column names by removing spaces,
# converting to lowercase, and replacing spaces with underscores.
def clean_column_names(df):

    df.columns = (
        df.columns
        .str.strip()
        .str.lower()
        .str.replace(" ", "_")
    )

    return df


# This function removes extra whitespace from text columns
# because inconsistent formatting makes analysis difficult.
def strip_whitespace(df):

    # Clean product names
    if "prodname" in df.columns:
        df["prodname"] = df["prodname"].astype(str).str.strip()

    # Clean category values
    if "category" in df.columns:
        df["category"] = (
            df["category"]
            .astype(str)
            .str.strip()
            .str.replace('"', '')
        )

    return df
    