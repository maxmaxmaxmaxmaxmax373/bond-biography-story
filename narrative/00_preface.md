---
title: "Preface"
---

(sec-preface)=
# Preface

This is a book that two people wrote, 144 years apart.

In 1881, **Rafael A. Bayley**, a clerk in the U.S. Treasury Department, completed *The National Loans of the United States, From July 4, 1776, to June 30, 1880*. The Tenth Census of the United States had asked him for an authoritative compilation of every loan the federal government had ever floated, with full statutory references, narrative accounts, and tabulated issues and redemptions. Bayley delivered it. In his August 1, 1881 letter of transmittal to Treasury Secretary William Windom, he wrote with quiet pride about the work he and his fellow-worker David S. Green had done:

> I take great pleasure in acknowledging my indebtedness… The late David S. Green was my fellow-worker in the laborious searchings through documents, old and new, bringing to the work great intelligence, zeal, and industry. I trust that the information furnished in these sheets may be promotive of a more general knowledge of our fiscal history, and more especially of the early financial struggles of our government, and that, as a work of reference, the compilation may be useful to many persons in official life.[^bayley-letter]

[^bayley-letter]: Bayley, R. A., letter of transmittal to Hon. Wm. Windom, Secretary of the Treasury, August 1, 1881, in *The National Loans of the United States* (Washington: Government Printing Office, 1881).

He was right. For 144 years, *The National Loans* has been the foundational reference for anyone trying to reconstruct what the United States owed, when, to whom, and on what terms. Every subsequent history of American public finance — from Davis Rich Dewey's 1903 *Financial History of the United States* to Paul Studenski and Herman Krooss's 1952 textbook to recent quantitative work by Robert Wright, Richard Sylla, and others — has drawn on Bayley's tables and statute citations. He is the spine of the literature.

But Bayley wrote in 1881, and he wrote as a Treasury insider. He had access to the official record — the statute books, the loan ledgers, the redemption schedules — but not to the secondary market. He could tell you that the Five-Twenties of 1862 were authorized by the Act of February 25, 1862 (12 Statutes, 345), that they were issued at par in \$50, \$100, \$500, and \$1,000 denominations, that subscriptions exceeded the authorization by \$11,000,000, and that ultimately \$514,771,600 face value were placed. What he could not tell you was how those bonds traded month by month after they left the Treasury — at what discount, in response to what events, with what volatility.

In 2025, **Jonathan Payne, Andrew Szoke, George Hall, and Thomas Sargent** completed the work that complements Bayley's. The **Hall–Payne–Sargent Bond Database** is a meticulous monthly compilation of secondary-market prices and outstanding quantities for some 2,857 federal bond issues spanning 1776 to 1960, drawn from contemporary financial periodicals and re-collated to modern data-engineering standards. Where Bayley wrote the political and statutory story of American federal debt, Hall–Payne–Sargent wrote the financial one.

This book reads them in counterpoint.

## The two voices

The 26 bonds biographized in these pages are presented in a hybrid form. Each biography opens with Bayley's framing — his statutory citation, his narration of the political circumstances, the figures he tabulated. Modern paragraphs follow without break, extending what Bayley wrote toward what we now know that he could not have known: how the secondary market priced his bonds; what the volatility tells us in retrospect; how the bond connects to others in the family; what its long downstream legacy turned out to be.

Bayley's words appear as block-quotations, attributed to him by section and statute. Statutes are cited in his own format — `12 Statutes, 345` — preserving the legal-research apparatus he built. The modern paragraphs that follow are clearly his successors, not his replacements. We are reading with him, not over him.

In a few places the two voices disagree. Where Bayley reports a final issuance figure that does not quite match the database's cumulative outstanding quantity — for instance, on the 1862 Five-Twenties, Bayley gives \$514,771,600 while the database peaks at \$514,773,800 — we note the discrepancy and let it stand. Bayley's official records and the contemporary press did not always reconcile to the dollar; this is itself a feature of 19th-century fiscal data, not a bug to be sanded over.

## The story line

Why pair them at all? Because the 26 bonds chosen for this book, taken together, tell a single coherent story: the **construction, breakdown, and reconstruction of American sovereign credit** between 1789 and 1907. The story has three acts.

The first act begins with **Alexander Hamilton's 1790 funding system** — the Six Per Cent, Three Per Cent, and Deferred Six Per Cent Stocks of 1790 — which transformed a chaotic mass of defaulted Revolutionary debt into standardized, marketable, federally-guaranteed securities. Within a decade the United States had moved from a credit-doubtful new republic into one of the more reliable sovereign borrowers in the Atlantic world. The act ends with **Albert Gallatin's debt-reduction program** culminating in the Jacksonian extinguishment of 1835 — the only moment in American history when the federal debt has been zero.

The second act is the antebellum era, marked by relatively easy borrowing for the Mexican War and the territorial purchases that followed (the Louisiana Purchase financing of 1804 and the Texas Indemnity of 1851 sit at this hinge), and ending in the catastrophic **Treasury Notes of 1860** — a bond issued at 9% during the secession crisis when New York banks would not lend at any conventional rate.

The third act is the **Civil War transformation** and its long sequel. Here Bayley's voice rises in volume, because he was writing about events still nearly within living memory. The Five-Twenties of 1862, the Ten-Forties of 1864, the Consols of 1865, and the great Funding Act refundings of 1870 — the 4.5% Loan of 1891 and the 4% Loan of 1907 — collectively accomplished what would once have seemed impossible: financing a war ten times more expensive than anything the country had ever attempted, then refinancing the resulting debt into instruments cheap enough that the federal interest burden fell faster than the debt itself was retired.

When the 4% Loan of 1907 was finally redeemed in 1907 — the very last bond in this book's sweep — the Panic of 1907 was already brewing, and within six years the Federal Reserve System would be in place. The Hamilton-Gallatin-McCulloch-Sherman world of debt management was passing into the world that Liberty Loans, the Treasury bill, and the Fed would inhabit. This book ends just as that transition begins.

## How to read

You can read the book cover-to-cover. The [Grand Arc](01_grand_arc.md) essay is designed for that purpose, and the era overviews provide further connective tissue. But each of the 26 bond biographies is also self-contained. Dip in wherever a particular bond catches your interest — the [Five-Twenties of 1862](../part3_civil_war_post/02_five_twenties_1862.ipynb) for the Civil War; the [Six Per Cent Stock of 1790](../part1_early_republic/03_six_per_cent_stock_1790.ipynb) for the founding; the [Loan of 1848](../part2_antebellum/03_loan_1848.ipynb) for an unusually clean window onto the antebellum financial cycle. The cross-references at the end of each biography will lead you onward.

For technical readers, the embedded Jupyter notebooks expose every chart's underlying code. Clone the repository, install the Python dependencies, and you can re-run any analysis on your own copy of the database. The data dictionary in [Appendix B](../appendix/B_data_dictionary.md) explains what each field means.

What we hope, in the end, is that Bayley would have approved. He wrote in 1881 that he hoped his work would "be promotive of a more general knowledge of our fiscal history." A century and a half later, with the modern database now matching his statutory archive month-by-month, that wish remains the animating spirit of this volume.
