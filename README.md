# The Bond Biographies of the United States, 1789–1907

A MyST Markdown book pairing Rafael A. Bayley's *The National Loans of the United States* (1881) with the modern Hall–Payne–Sargent Bond Database (2025), producing 26 illustrated bond biographies plus narrative essays and appendices.

## Build locally

Requires [`mystmd`](https://mystmd.org) and a Python environment with `pandas`, `matplotlib`, `numpy`, and `tables` (for HDF5 reading).

```bash
# install MyST
npm install -g mystmd

# install python dependencies for the embedded notebooks
pip install pandas matplotlib numpy tables

# build the book
myst build --html

# serve it locally
myst start
```

## Project structure

```
bond-biography-story/
├── myst.yml                 # MyST project configuration
├── index.md                 # Landing page
├── data/BondDF.h5           # Hall-Payne-Sargent database (notebooks read this)
├── narrative/               # 4 spine essays (preface, grand arc, method, conclusion)
├── part1_early_republic/    # 11 bond biographies + era overview/synthesis
├── part2_antebellum/        #  5 bond biographies + era overview/synthesis
├── part3_civil_war_post/    # 10 bond biographies + era overview/synthesis
└── appendix/                # 4 reference appendices
```

## Sources

- **Primary (1881)**: Bayley, R. A. *The National Loans of the United States, From July 4, 1776, to June 30, 1880*. Washington: Government Printing Office. A digital MyST edition is available at the companion `bayley-myst/` project.
- **Database (2025)**: Payne, J., Szoke, A., Hall, G. & Sargent, T. *Hall–Payne–Sargent Bond Database* — secondary-market price and outstanding-quantity series for U.S. federal bonds.

## Deployment

A GitHub Actions workflow at `.github/workflows/deploy.yml` builds the MyST site and deploys to GitHub Pages. To publish, push the project to a new public repository and ensure Pages is configured to deploy from GitHub Actions.

## License

The Bayley primary source is in the public domain. The modern commentary, charts, and editorial apparatus in this volume are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
