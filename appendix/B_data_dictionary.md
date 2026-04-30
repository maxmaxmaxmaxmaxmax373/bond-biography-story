---
title: "Appendix B — Data Dictionary"
---

(sec-appendix-data-dictionary)=
# Appendix B — Data Dictionary

This appendix documents the structure of the Hall–Payne–Sargent Bond Database (`data/BondDF.h5`) as accessed by the notebooks in this book. The database is distributed in HDF5 format and is read by the standard pandas `HDFStore` interface.

## Database files

The database file is `data/BondDF.h5`, located at the project root's `data/` subdirectory. It contains three main DataFrames, accessed by HDF5 keys:

| Key | DataFrame | Shape | Description |
|---|---|---|---|
| `BondList` | static metadata | ~2,857 rows | One row per bond issue, indexed by Bond ID (L1). |
| `BondQuant` | quantity time series | wide format | Monthly outstanding-quantity series. Bond IDs as columns; dates as rows. |
| `BondPrice` | price time series | wide format | Monthly secondary-market price series. Bond IDs as columns; dates as rows. |

The notebooks in this book always immediately transpose `BondQuant` and `BondPrice` to get a more convenient access pattern:

```python
BondQuant_T = BondQuant.transpose()
BondPrice_T = BondPrice.transpose()

# Access a specific bond's price time series:
p = BondPrice_T.loc[(20101, 'Average')]   # Five-Twenties of 1862, average price
```

## `BondList` columns (selected)

The `BondList` DataFrame has many columns; the notebooks in this book read primarily the following:

| Column | Type | Description |
|---|---|---|
| `Treasury's Name Of Issue` | str | Official Treasury name (e.g., "Five-Twenties of 1862"). |
| `Authorizing Act` | str | Statutory authorization (e.g., "February 25, 1862"). |
| `Authorizing Act Date` | datetime | Parsed authorizing-act date. |
| `First Issue Date` | datetime | First issuance date recorded in the database. |
| `Term Of Loan` | str | Term description (e.g., "5 or 20 yrs"). |
| `Redeemable After Date` | datetime | First call/redemption-eligible date (NaT if not callable). |
| `Payable Date` | datetime | Final maturity date (NaT if perpetual). |
| `Coupon Rate` | float | Annual coupon rate as a percentage (e.g., 6.0 for 6%). |
| `Coupons Per Year` | float | Coupon-payment frequency (typically 2 for semi-annual, 4 for quarterly, 0 for at-maturity). |
| `Callable` | float | 1.0 if callable, 0.0 otherwise. |
| `Coin` | float | 1.0 if interest paid in coin, 2.0 if both interest and principal in coin, 0.0 if not. |
| `Price Sold` | float | Issuance price as a fraction of par (e.g., 1.00 for par, 0.88 for 12% discount). |
| `Category L1` | str | High-level category (e.g., "Interest Bearing"). |
| `Category L2` | str | Marketability category (e.g., "Marketable"). |
| `Category L3` | str | Instrument-class category (e.g., "Long Term Bond", "Treasury Note : Pre 1920"). |

## `BondQuant_T` index structure

After transposition, the quantity DataFrame has a 2-level MultiIndex on its index axis:

```python
BondQuant_T.index.names = ['Bond ID', 'Series Type']
```

Where `Series Type` is one of:

| Series Type | Meaning |
|---|---|
| `Total Outstanding` | Face value of bonds outstanding on the Treasury's books. Includes some long-tail residuals after substantive redemption. |
| `Public Holdings` | Face value held by private investors (excluding Treasury sinking-fund repurchases). |

The columns are dates (typically end-of-month).

```python
# Example: get Total Outstanding for Five-Twenties of 1862
q = BondQuant_T.loc[(20101, 'Total Outstanding')]
q = q[q.notna()]
print(q.head())
```

## `BondPrice_T` index structure

Similarly, after transposition the price DataFrame has a 2-level MultiIndex:

```python
BondPrice_T.index.names = ['Bond ID', 'Statistic']
```

Where `Statistic` is one of:

| Statistic | Meaning |
|---|---|
| `Average` | Monthly average traded price. The notebooks in this book use this as the canonical price series. |
| `High` | Monthly high. (May be missing for sparse-traded issues.) |
| `Low` | Monthly low. (May be missing for sparse-traded issues.) |

The columns are dates (typically end-of-month, expressed as `datetime64[ns]`).

## Data quirks the reader should know

### 1. Long retirement tails

Many bonds have `Total Outstanding` series that continue years or decades past the bond's substantive retirement, with residual balances of a few hundred or thousand dollars. This reflects unpresented bonds, lost certificates, or accounting carry-overs on Treasury books. Where the notebooks in this book quote a "final database observation", that observation may be a residual rather than a meaningful balance.

### 2. Public Holdings vs. Total Outstanding

`Public Holdings` is typically smaller than `Total Outstanding` because the Sinking Fund and Treasury repurchases held some bonds outside private-investor hands. For most of the bonds in this book, the two series move together but with `Public Holdings` somewhat below `Total Outstanding` in years of active sinking-fund operations.

### 3. Price series gaps

Some bonds have sparse or absent price series — particularly:
- Bonds held primarily by banks or sinking-fund operations (e.g., the Mexican Indemnity Stock).
- Short-term at-maturity instruments (e.g., the One Year Notes of 1863).
- Refunding-only instruments issued directly to specific holders (e.g., the Exchanged and Converted Stocks of 1807).

Where price data is absent, the relevant biography includes a note indicating that the database does not contain a secondary-market price series for that bond.

### 4. Coupon-rate discrepancies

A handful of bonds in `BondList` have NaN or unusual `Coupon Rate` values — typically aggregated rows that combine multiple issues (e.g., "3.5%, 4%, and 4.25% First Liberty Loan" in the WWI-era data). The 26 bonds biographized in this book all have well-defined coupon rates, but readers running the data themselves should be aware of these aggregate rows.

### 5. Nominal dollars

All quantity figures are in **nominal dollars of the period** — they are not inflation-adjusted to any base year. A \$10 million bond in 1813 represents a much larger fraction of the federal budget than a \$10 million bond in 1907. The biographies and era overviews note this contextually where it matters.

## Cross-reference: `BondList[id]` lookup

A useful one-liner for inspecting any bond:

```python
import pandas as pd
import warnings; warnings.filterwarnings('ignore')

store = pd.HDFStore('data/BondDF.h5', mode='r')
BondList = store['BondList']
store.close()

bond_id = 20101  # Five-Twenties of 1862
print(BondList.loc[bond_id])
```

This dumps every column for the specified bond, including ones the notebooks may not display. The full `BondList` schema documents every column; consult the Hall-Payne-Sargent database documentation distributed with the source data for complete field descriptions.

## Source citation

> Payne, J., Szoke, A., Hall, G. & Sargent, T. (2025). *Hall–Payne–Sargent Bond Database* — secondary-market price and outstanding-quantity series for U.S. federal bonds, 1776–1960.

A working-paper description of the database's compilation methodology is available from the authors. The version included in this book at `data/BondDF.h5` is a snapshot from 2025; readers wishing to use the most current version of the database should consult the Hall-Payne-Sargent project directly.
