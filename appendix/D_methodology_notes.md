---
title: "Appendix D — Methodology Notes"
---

(sec-appendix-methodology)=
# Appendix D — Methodology Notes

This appendix records editorial and computational decisions made during the construction of this book. Most of these are minor; a few are worth flagging for readers who want to reproduce or verify particular results.

## Editorial conventions

### Bayley quotation style

Bayley quotations are reproduced verbatim from the digital MyST edition of *The National Loans of the United States* (1881), located in the companion `bayley-myst/paper/ch0X_*.md` files. We have made the following minor stylistic decisions:

- **Statute citations** preserve Bayley's format (`12 Statutes, 345`).
- **Money figures** preserve Bayley's nineteenth-century formatting where possible: `\$ 514,771,600` rather than `$514.8 million`. Where a figure is reproduced in modern decimal form (e.g., in the bond-features tables), the conversion is documented in the surrounding text.
- **Spelling** preserves Bayley's text as published, including period-typical usage (e.g., "five-twenties" rather than "5-20s"; "Five-Twenties of 1862" rather than "Five Twenties of 1862").
- **Block-quotation breaks**: where Bayley's prose runs across multiple paragraphs, we preserve the original paragraph breaks within the block-quote. Where we excerpt only a sentence or two from a longer passage, the excerpt is delimited at sentence boundaries rather than mid-sentence.

### Modern commentary attribution

Modern commentary in the bond biographies and narrative essays is **collective editorial voice** — there is no single author of any individual passage. Where particular interpretive judgments draw on a specific scholarly source, the source is cited inline or in the per-bond References section.

### Cross-references

Internal cross-references use MyST's `{ref}` syntax, with section anchors of the form `(bond-XXXXX-name)=` for individual bonds and `(sec-...)=` for narrative pages. The cross-reference target is the bond's official MyST anchor; the displayed text is conventionally a markdown link with descriptive label.

## Chart conventions

### Color palette

Period-shading colors are applied consistently across all chart types in all bond biographies:

| Period | Color | RGB |
|---|---|---|
| War of 1812 | red | `#e74c3c` |
| Civil War | red | `#e74c3c` |
| Mexican-American War | red | `#e74c3c` |
| Panic of 1819 | purple | `#9b59b6` |
| Panic of 1857 | purple | `#9b59b6` |
| Panic of 1873 / Long Depression | purple | `#9b59b6` |
| Panic of 1893 | purple | `#9b59b6` |
| Reconstruction era | orange | `#f39c12` |
| Secession Crisis | orange | `#f39c12` |
| Bond price (line) | dark slate | `#2c3e50` |
| Quantity (line) | blue | `#3498db` or `#1f77b4` |

### Period boundary dates

Where a period's start/end date is not unambiguous in the literature, this book uses the following conventions:

- **War of 1812**: June 18, 1812 (declaration) – February 18, 1815 (ratification of Treaty of Ghent).
- **Mexican-American War**: April 25, 1846 (Thornton Affair) – February 2, 1848 (Treaty of Guadalupe Hidalgo).
- **Civil War**: April 12, 1861 (Fort Sumter) – May 9, 1865 (Confederate forces surrender at Memphis, after Appomattox on April 9).
- **Panic of 1819**: January 1, 1819 – December 31, 1821.
- **Panic of 1857**: August 24, 1857 (Ohio Life Insurance failure) – December 31, 1859.
- **Panic of 1873 / Long Depression**: September 18, 1873 (Jay Cooke & Co. failure) – March 1, 1879.
- **Panic of 1893**: May 5, 1893 – June 30, 1897.
- **Reconstruction**: May 10, 1865 – March 31, 1877 (end of Hayes-Tilden compromise).
- **Secession Crisis**: December 20, 1860 (South Carolina secession) – April 12, 1861 (Fort Sumter).

### Chart code reuse

Each notebook generates the same standard set of charts using a small Python helper pattern. The helper code is duplicated across notebooks rather than imported — this was a deliberate choice: each notebook is self-contained and can be executed independently of the others.

## Database access

### Reading the HDF5 file

All notebooks use the following pattern to read the database:

```python
import pandas as pd
import warnings; warnings.filterwarnings('ignore')

store = pd.HDFStore('../data/BondDF.h5', mode='r')
BondList = store['BondList']
BondQuant = store['BondQuant']
BondPrice = store['BondPrice']
store.close()

BondQuant_T = BondQuant.transpose()
BondPrice_T = BondPrice.transpose()
```

The `'../data/BondDF.h5'` path resolves correctly when notebooks are run from any of the three part subdirectories. The data file lives at `bond-biography-story/data/BondDF.h5`.

### Caveats on `BondQuant_T` access

The transposed-quantity DataFrame can return `Series` or `DataFrame` depending on whether a single Bond ID has one or multiple Series Type entries. Most notebooks handle this with a `try / except KeyError` block:

```python
try:
    s = BondQuant_T.loc[(bond_id, 'Total Outstanding')]
    s = s[s.notna()].sort_index()
    if len(s) > 0:
        ax.plot(s.index, s.values / 1e6, ...)
except KeyError:
    pass
```

This pattern is used consistently across all 26 notebooks.

### Discrepancy between Bayley figures and database

Where Bayley's tabulated issuance or redemption figures differ from the database's monthly observations, the discrepancy is typically smaller than 0.1% of the headline figure. The most common sources of difference:

1. **Fiscal-year vs. calendar-year accounting.** Bayley reports end-of-fiscal-year balances (June 30 for the period this book covers); the database reports end-of-month balances.
2. **Capitalized accrued interest.** Some bonds were issued with accrued interest that Bayley counts as principal and the database may attribute to a different category.
3. **Rounding of large totals.** Bayley occasionally rounds to the nearest \$50 or \$100; the database carries more decimal places.

Where a bond's headline statistic is mentioned in both this book's commentary and Bayley's narrative, we use Bayley's figure for narrative continuity and note any database discrepancy parenthetically.

## Coverage decisions

### Why these 26 bonds?

The 26 bonds biographized in this book were selected by the editor in coordination with their advisor as a representative cross-section of the 1789–1907 federal debt. Selection criteria:

1. **Major issuance events** that Bayley treats at length — every Bayley section that runs to more than two pages of his narrative is represented.
2. **Pivotal political moments** — the Louisiana Purchase, the Compromise of 1850, the secession crisis, the Civil War, the 1870 refunding.
3. **Database support** — bonds for which the Hall-Payne-Sargent database provides at least quantity series (price series preferred, but not strictly required).
4. **Family completeness** — where Bayley treats multiple bonds as a single family (e.g., the three 1790 Stocks, the Funded Loans of 1881/1891/1907), the family is treated together rather than partially.

### What is not covered

Beyond the bonds listed in the [Bayley Crosswalk Appendix A](A_bayley_crosswalk.md), this book does not biographize:

- The Holland Loans of 1782–1794 (foreign Revolutionary debt, before federal authority).
- The Subscription Loan of 1791 and most other small early-republic loans.
- Most of the various smaller War of 1812 instruments.
- The Treasury Notes of 1837–1845.
- The 5% Loan of 1881 (Bond ID 20119), the Loan of 1858, the Loan of 1860, and the Loan of February 1861.
- Currency instruments (Greenbacks, Coin Certificates, Refunding Certificates, Silver Certificates).
- The Spanish-American War financings (Bond ID 20130, 20132, 20133).

A future expanded edition could add any or all of these. The notebook template developed for this book is reusable for any bond in the database.

## Reproducibility

### Building from source

To reproduce the book locally:

```bash
cd Bayley_experiment/bond-biography-story
pip install pandas matplotlib numpy tables jupyter
npm install -g mystmd
myst build --html
myst start
```

The build will execute every notebook against `data/BondDF.h5` and re-render all charts. A complete build takes a few minutes on typical hardware.

### Verifying notebook execution

Each notebook can be re-executed individually:

```bash
cd part1_early_republic
jupyter nbconvert --to notebook --execute 03_six_per_cent_stock_1790.ipynb --output _test.ipynb
```

A successful execution produces an `_test.ipynb` of roughly 600 KB (600,000 bytes) with embedded chart images. If execution fails, the most likely cause is missing `data/BondDF.h5` (verify with `ls ../data/`).

### Cross-reference auditing

To verify that all `{ref}` cross-references resolve to existing anchors:

```bash
grep -rn "{ref}" . | grep -v _build/
grep -rn "(bond-" . | grep -v _build/
```

Compare the targets used in `{ref}` calls to the anchors defined elsewhere; every target should appear at least once on the right-hand side.

## License & attribution

- **Bayley primary source** is in the public domain (1881 U.S. Government publication).
- **Hall-Payne-Sargent database** is distributed by its authors with their preferred citation.
- **Modern commentary, charts, structural editorial work, and apparatus** in this book are released under [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

When citing this book, please use a form similar to:

> *The Bond Biographies of the United States, 1789–1907: An Illustrated Reading of Bayley's National Loans (1881) with the Hall–Payne–Sargent Database.* MyST Markdown edition (2026).

with appropriate URL once the book is hosted on GitHub Pages.
