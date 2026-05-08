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
    # This function handles missing values in price and quantity columns.
# Missing values can cause issues during calculations and analysis.
def handle_missing_values(df):

    # Convert columns to numeric
    df["price"] = pd.to_numeric(df["price"], errors="coerce")
    df["qty"] = pd.to_numeric(df["qty"], errors="coerce")

    # Remove rows with missing prices
    df = df.dropna(subset=["price"])

    # Fill missing quantities with 0
    df["qty"] = df["qty"].fillna(0)

    return df


# Copilot-assisted function:
# Remove rows with invalid negative values because
# negative prices and quantities are likely data entry errors.
def remove_invalid_rows(df):

    df = df[df["price"] >= 0]
    df = df[df["qty"] >= 0]

    return df


# Main program execution
if __name__ == "__main__":

    raw_path = "data/raw/sales_data_raw.csv"
    cleaned_path = "data/processed/sales_data_clean.csv"

    # Load raw dataset
    df_raw = load_data(raw_path)

    # Clean column names
    df_clean = clean_column_names(df_raw)

    # Remove extra whitespace
    df_clean = strip_whitespace(df_clean)

    # Handle missing values
    df_clean = handle_missing_values(df_clean)

    # Remove invalid rows
    df_clean = remove_invalid_rows(df_clean)

    # Save cleaned dataset
    df_clean.to_csv(cleaned_path, index=False)

    print("Cleaning complete. First few rows:")
    print(df_clean.head())
    