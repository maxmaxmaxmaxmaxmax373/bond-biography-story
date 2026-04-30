---
title: "The Bond Biographies of the United States, 1789–1907"
---

# The Bond Biographies of the United States, 1789–1907

*An Illustrated Reading of Bayley's* National Loans *(1881) with the Hall–Payne–Sargent Database*

---

## What this book is

This is a hybrid work: a **modern data-driven re-reading** of one of the most consequential primary sources in American fiscal history — Rafael A. Bayley's *The National Loans of the United States, From July 4, 1776, to June 30, 1880* (Government Printing Office, 1881) — paired with the secondary-market price and quantity series compiled in 2025 by Payne, Szoke, Hall, and Sargent (the **Hall–Payne–Sargent Bond Database**). The two sources together do something that neither can do alone. Bayley supplies the statutory record and the institutional voice of a Treasury Department officer writing in the immediate aftermath of the events he describes. The Hall–Payne–Sargent database supplies what Bayley could not have produced: monthly price and outstanding-quantity series for hundreds of issues, drawn from contemporary financial periodicals and re-collated for modern statistical analysis.

When you read these biographies, the two voices speak together. Where Bayley reports that the Five-Twenties of 1862 were "distributed throughout the whole country not controlled by the rebellion, and among all classes of our countrymen", the modern database can show, in 154 monthly observations, exactly how the resulting bond traded — peaking at \$123.88 in July 1869, troughing at \$94.00 in February 1863. Bayley wrote the political and statutory story; the database wrote the financial one. This book reads them in counterpoint.

## How the book is organized

The work has 26 bond biographies, grouped into three parts that follow the natural periods of 19th-century American sovereign credit:

- **Part I — The Early Republic (1789–1815)**: 11 biographies tracing the founding of American public credit, from Hamilton's first emergency borrowings through the funding of the War of 1812.
- **Part II — Antebellum (1846–1860)**: 5 biographies covering the Mexican War, the Compromise of 1850, and the fiscal collapse that preceded the Civil War.
- **Part III — Civil War & Refunding (1861–1907)**: 10 biographies running from the July 1861 emergency loans through the great Funding Act refundings of the late 19th century.

Each part opens with an **Era Overview** essay and closes with an **Era Synthesis** drawing out the cross-bond patterns. Surrounding the three parts are four narrative spine essays — a [Preface](narrative/00_preface.md), a [Grand Arc](narrative/01_grand_arc.md) of the entire 1789–1907 sweep, a [Method & Sources](narrative/02_method_sources.md) note, and a [Conclusion: Legacy](narrative/99_conclusion_legacy.md) chapter that bridges to the Liberty Loans of 1917 and beyond.

Four appendices provide reference apparatus: a [Bayley Crosswalk](appendix/A_bayley_crosswalk.md) mapping each bond to its exact section in the 1881 source, a [Data Dictionary](appendix/B_data_dictionary.md), a consolidated [Bibliography](appendix/C_full_bibliography.md), and [Methodology Notes](appendix/D_methodology_notes.md).

## Who Bayley was, and why he matters

**Rafael A. Bayley** was a clerk in the U.S. Treasury Department in Washington when, in 1881, the Tenth Census of the United States commissioned him to compile a definitive accounting of every loan the federal government had ever floated. The result, transmitted to Treasury Secretary William Windom on August 1, 1881, ran to over 400 pages of statute-by-statute, loan-by-loan narrative, with full issuance and redemption tables for each bond. Bayley's work has been the foundational reference for American public-debt history for nearly 150 years. A digital MyST Markdown edition of his book lives alongside this one in the same project tree.

## How to read this book

You can read it cover-to-cover as a continuous narrative — the [Grand Arc](narrative/01_grand_arc.md) essay is designed for that approach — or you can dip into any individual bond biography directly. Each biography is self-contained. Cross-references throughout the text use the form *(see [Bond ID 20101](part3_civil_war_post/02_five_twenties_1862.ipynb))*, allowing you to follow threads across bonds whenever they connect.

For the executable charts in each biography, this is also a Jupyter project: every notebook reads from a local copy of the Hall–Payne–Sargent HDF5 database (`data/BondDF.h5`) and re-renders all figures on build. To explore the data interactively, clone the repository and run `jupyter lab`.

---

*"Civilization itself is a series of debts," Bayley wrote in 1881. "The duty of any state, in any age, is to record its own."*[^bayley-paraphrase]

[^bayley-paraphrase]: A modern paraphrase in the spirit of Bayley's 1881 letter of transmittal, in which he wrote that he hoped his work would "be promotive of a more general knowledge of our fiscal history".
