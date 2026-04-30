---
title: "Method & Sources"
---

(sec-method-sources)=
# Method & Sources

This book is methodologically simple but unusual: it pairs a 19th-century primary source with a 21st-century database, and lets each speak in its own voice within the body of every bond biography. The mechanics are worth a brief note.

## The two anchor sources

### Bayley, *The National Loans of the United States* (1881)

The primary-source spine is **Rafael A. Bayley's** *The National Loans of the United States, From July 4, 1776, to June 30, 1880* (Washington: Government Printing Office, 1881). Compiled at the request of the Tenth Census of the United States, transmitted to Treasury Secretary William Windom on August 1, 1881, the work runs to over 400 pages and contains, for every federal loan from 1776 through 1880:

- The full statutory citation (e.g., `12 Statutes, 345`)
- A narrative account of the political and fiscal circumstances that produced the loan
- The bond's terms (coupon, term, redemption schedule)
- Tabulated annual issues and redemptions
- Where applicable, full quotations of the authorizing statute

The book has been the foundational reference work for American public-debt history for nearly 150 years. A digital MyST Markdown edition of Bayley — produced from the Internet Archive's scan of the Cornell University Library copy — is maintained in the companion `bayley-myst/` project alongside this one. Throughout this book, when we quote Bayley directly, the quotation is set as a markdown blockquote and is referenced by chapter and approximate page number; the curious reader can locate every quoted passage in the digital edition.

### The Hall–Payne–Sargent Bond Database (2025)

The data-analytic spine is the **Hall–Payne–Sargent Bond Database**, compiled by Jonathan Payne, Andrew Szoke, George Hall, and Thomas Sargent in 2025 and distributed in HDF5 format (`BondDF.h5`). The database covers 2,857 federal bond issues spanning 1776 to 1960 and provides, for most issues:

- **`BondList`**: Static metadata — bond name, authorizing act, first issue date, redemption dates, coupon rate, callability, denomination, and so on.
- **`BondQuant`**: Monthly outstanding-quantity time series, both "Total Outstanding" (face value of issued bonds) and "Public Holdings" (amount in private-investor hands).
- **`BondPrice`**: Monthly secondary-market price observations, with high/low/average and trade-volume fields where available.

The database is the first systematic compilation of monthly secondary-market data for 19th-century U.S. federal debt. Its construction draws on contemporary financial periodicals — the *Bankers' Magazine*, the *Commercial and Financial Chronicle*, the *American Railroad Journal*, and others — re-collated to modern data-engineering standards. The database is described in the working paper Payne, J., Szoke, A., Hall, G., and Sargent, T. (2025), and a copy is included in this project at `data/BondDF.h5`.

## The interleave method

In the 26 bond biographies that follow, the two sources speak together in a single narrative. The convention is:

- **Bayley's prose** appears as block-quotes:

> The success of this loan was remarkable. Secretary Chase having used every exertion to provide for its general distribution among the people.[^bayley-example]

[^bayley-example]: Bayley, *National Loans*, ch. 4, on the Five-Twenties of 1862.

- **Modern commentary** is plain text, immediately following the Bayley quotation, extending or contextualizing it. We make no attempt to re-write Bayley; we let his sentences stand as he wrote them and add the analytical lens of 144 years' subsequent scholarship.

- **Statute citations** preserve Bayley's format: `12 Statutes, 345` for Volume 12 of the Statutes at Large, page 345. Modern cross-references to other bonds in this book use markdown links: *(see [Loan of 1848](../part2_antebellum/03_loan_1848.ipynb))*.

- **Tabular data** from Bayley (issuance and redemption tables) is reproduced where useful and compared to the database's monthly series. Where the two diverge by more than rounding amounts, we note the discrepancy explicitly. Bayley's tables sometimes report end-of-fiscal-year balances; the database reports calendar-month-end balances. They do not always reconcile to the dollar.

## Chart conventions

Every biography contains a standard set of charts, generated from the database:

- **Lifecycle Timeline** — a horizontal timeline of authorizing-act, first issue, key historical events, redemption window, and final retirement.
- **Outstanding Quantity** — line chart of `Total Outstanding` and `Public Holdings` against time, with period shading (war years, financial panics) overlaid.
- **Secondary Market Price** — line chart of monthly average price, with extreme observations annotated and period shading overlaid.
- **Price and Quantity Together** — dual-axis chart for visual cross-correlation.
- **Volatility & Drawdown** — rolling 12-month standard deviation of price, plus a drawdown-from-peak shaded region.

Period shading uses consistent colors across the book:

| Period | Color |
|---|---|
| Civil War | red (#e74c3c) |
| War of 1812 | red (#e74c3c) |
| Mexican-American War | red (#e74c3c) |
| Long Depression / Panic of 1873–79 | purple (#9b59b6) |
| Panic of 1819 | purple (#9b59b6) |
| Panic of 1857 | purple (#9b59b6) |
| Panic of 1893 | purple (#9b59b6) |
| Reconstruction era | orange (#f39c12) |
| Secession crisis | orange (#f39c12) |

These conventions were chosen to match the existing visualization style in the upstream `02-Bond-Biographies/` notebooks (see the [chapter_20162_1st_Liberty_Loan_enhanced.ipynb](../../02-Bond-Biographies/notebooks/enhanced_chapters/chapter_20162_1st_Liberty_Loan_enhanced.ipynb) template).

## What we have not done

A note on omissions. This book contains 26 bond biographies, not 2,857. The bonds were chosen by the editor in coordination with their advisor as a representative cross-section of the 1789–1907 federal debt — major issues, illustrative families, and pivotal moments — drawn from the Bayley source and matched to the database. We have not biographized the Holland Loans (Bond IDs 20009–20018), the various small Treasury Notes of the 1830s and 1840s, the Spanish-American War financing, or the Panama Canal Loans. These would all be worthy subjects, and the database supports them; this book does not.

We also have not attempted to build new economic models, run new statistical tests, or extend the Hall–Payne–Sargent database beyond what its authors published. The intellectual contribution here is **editorial and integrative**: putting Bayley's voice and the modern data record into a single readable document. The serious quantitative work on this data has been done elsewhere and continues to be done; this book points readers toward it.

## A request to the reader

If you find errors, please let us know. Bayley wrote in 1881 that "the responsibility for any errors that may exist in this work must rest entirely upon me, but I think it proper to say that the statements have been most carefully verified." The same is true of the modern commentary in this volume. The Bayley quotations are taken verbatim from the digital MyST edition; the price and quantity figures are taken directly from `BondDF.h5`. Where we have made interpretive judgments — on cause-and-effect, on legacy, on the comparative weight of bonds — those judgments are our own, and corrections are welcome.

References to Bayley's primary source can be located via the [Bayley Crosswalk in Appendix A](../appendix/A_bayley_crosswalk.md). Database fields are explained in the [Data Dictionary in Appendix B](../appendix/B_data_dictionary.md). Methodological decisions are recorded in [Appendix D](../appendix/D_methodology_notes.md).
