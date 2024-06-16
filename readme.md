# Readme

## Folders/Files description
- `input`: files compiled by Green and Han
  - `input/_characteristics.csv`: metadata of characteristics (only the ones used in Han et al.)
  - `input/green.csv`: Green's data (variable `temp2` in his SAS code)
  - `input/han_et_al.pdf`: Han et al. pdf
- `output_direct`: Green's data separated monthly, and no other processing
  - `output_direct/YYYY-MM-DD.csv`: 
    - Green's data for the month of YYYY-MM, DD is the last day of the month
    - Rows: firms' gvkey (identifier), columns: characteristics and momentum
        - we currently do not have translation tables from gvkey to isin, sedol, etc. (one manually obtain by processing `input/green.csv`)
        - column `mom_1` = price(YYYY-MM-DD) / price(YYYY-(MM-1)-DD) - 1
        - columns `mom_n` = price(YYYY-(MM-1)-DD) / price(YYYY-(MM-n)-DD) - 1 for n > 1
  - `output_direct/_momentum.csv`:
    - monthly momentum for each firm
    - Rows: date, columns: firms' gvkey (identifier)
      -  row `YYYY-MM-DD` = price(YYYY-MM-DD) / price(YYYY-(MM-1)-DD) - 1
- `output_dropna`: folders of files from `output_direct` with cols/rows with missing values dropped
  - `output_dropna/simple`: files from `output_direct` with rows with missing values dropped
    - file structure, columns, and names are the same as in `output_direct`
  - `output_dropna/smart`: files from `output_direct` with columns with significant amount of missing values dropped, and rows with missing values dropped
    - file structure, columns, and names are the same as in `output_direct`
    - by comparing sizes of dataframes made by applying different dropna threshold, we find the optimised threshold for each month
    - see `smartdropna()` function in `common.py` file for more details
  - `output_dropna/smartexmom`: similar to `output_smartdropna`, but momentum columns are excluded from the dropna-ing
    - file structure, columns, and names are the same as in `output_direct`
    - by comparing sizes of characteristic dataframes made by applying different dropna threshold, we find the optimised threshold for each month
    - see `smartdropna()` function in `common.py` file for more details