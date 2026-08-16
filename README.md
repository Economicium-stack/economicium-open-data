# Economicium open data

16 economic and financial datasets as plain CSV. 18,106 rows in total.
Government and public-domain sources, each one named, licence-checked and dated.

No API key, no signup, no rate limit. Clone it, or link the raw file.

```bash
git clone https://github.com/Economicium-stack/economicium-open-data.git
```

Every file is also served over HTTPS at `https://economicium.com/data/<name>.csv`,
and as JSON at `https://economicium.com/data/<name>.json`. The JSON keeps the
original nesting plus source and licence metadata that a flat CSV cannot carry,
and it sends an open CORS header, so you can fetch it straight from a browser.

## The datasets

| File | What it is | Rows | Source |
|---|---|---|---|
| [`us-cpi-monthly.csv`](data/us-cpi-monthly.csv) | US CPI-U, monthly index | 1,361 | [U.S. Bureau of Labor Statistics](https://www.bls.gov/cpi/) |
| [`us-cpi-by-category.csv`](data/us-cpi-by-category.csv) | US CPI by expenditure group, monthly | 3,870 | [U.S. Bureau of Labor Statistics](https://www.bls.gov/cpi/) |
| [`ecb-fx-daily.csv`](data/ecb-fx-daily.csv) | ECB reference rates, daily by pair | 10,360 | [European Central Bank, via Frankfurter](https://www.frankfurter.dev/) |
| [`ecb-fx-latest.csv`](data/ecb-fx-latest.csv) | ECB reference rates, latest snapshot | 30 | [European Central Bank, via Frankfurter](https://www.frankfurter.dev/) |
| [`us-recession-indicators.csv`](data/us-recession-indicators.csv) | US recession indicators, monthly | 1,594 | [Federal Reserve Bank of St. Louis (FRED)](https://fred.stlouisfed.org/) |
| [`us-national-debt.csv`](data/us-national-debt.csv) | US national debt, monthly | 259 | [U.S. Department of the Treasury](https://fiscaldata.treasury.gov/datasets/debt-to-the-penny/) |
| [`us-mortgage-rate-30y.csv`](data/us-mortgage-rate-30y.csv) | US 30-year fixed mortgage rate, weekly | 146 | [Freddie Mac PMMS, via FRED](https://fred.stlouisfed.org/series/MORTGAGE30US) |
| [`us-i-bond-rates.csv`](data/us-i-bond-rates.csv) | US Series I savings bond rates | 57 | [U.S. Department of the Treasury, TreasuryDirect](https://www.treasurydirect.gov/savings-bonds/i-bonds/i-bonds-interest-rates/) |
| [`central-bank-policy-rates.csv`](data/central-bank-policy-rates.csv) | Central bank policy rates | 5 | [Each central bank, published directly](https://www.ecb.europa.eu/) |
| [`economic-calendar.csv`](data/economic-calendar.csv) | Economic release calendar | 232 | [National statistics agencies and central banks](https://fred.stlouisfed.org/) |
| [`euro-area-calendar.csv`](data/euro-area-calendar.csv) | Euro-area release calendar | 15 | [Eurostat](https://ec.europa.eu/eurostat/) |
| [`earnings-date-estimates.csv`](data/earnings-date-estimates.csv) | Earnings date estimates | 85 | [SEC EDGAR filing history (our derivation)](https://www.sec.gov/edgar) |
| [`crypto-staking-yields.csv`](data/crypto-staking-yields.csv) | Crypto staking yields | 4 | [Protocol issuance formulas applied to live on-chain totals (our computation)](https://ethereum.org/en/staking/) |
| [`irs-rmd-uniform-lifetime-table.csv`](data/irs-rmd-uniform-lifetime-table.csv) | IRS RMD uniform lifetime table | 48 | [Internal Revenue Service, Publication 590-B, Appendix B, Table III](https://www.irs.gov/publications/p590b) |
| [`nber-recessions.csv`](data/nber-recessions.csv) | NBER US recession chronology | 35 | [NBER recession dates via FRED (USREC)](https://fred.stlouisfed.org/series/USREC) |
| [`bitcoin-halvings.csv`](data/bitcoin-halvings.csv) | Bitcoin halving history | 5 | [Bitcoin blockchain, via mempool.space](https://mempool.space/) |

## Licensing, and why some things are missing

Every dataset here is a government work, public domain, or explicitly licensed
for redistribution. That bar is deliberately higher than the one for showing a
figure on a web page: publishing a number is one act, handing over the whole
series is another.

Two things are therefore **not** here:

- **Futures contract specifications.** Published by CME Group, which is neither
  public domain nor licensed for bulk redistribution.
- **Consensus forecasts.** Compiled by commercial vendors whose terms forbid
  free republication. This is also why the Economicium economic calendar has no
  expected-value column.

If a dataset you want is missing, the likeliest reason is that we could not
source it on terms that let us hand it to you.

## Attribution

Credit the originating agency first and Economicium second:

> BLS, via Economicium (economicium.com)

The underlying data is not ours to license. The compilation, the cleaning and
the consistent formatting are.

This product uses the FRED® API but is not endorsed or certified by the Federal
Reserve Bank of St. Louis.

## How this stays current

A GitHub Action pulls the published CSVs from economicium.com weekly and commits
anything that changed, so the files here track the live site rather than drifting
away from it. Each dataset's own refresh cadence is listed below.

## Dataset detail

### `us-cpi-monthly.csv`

The US consumer price index, every month back to 1913.

- **Columns:** `date, year, month, index_value`
- **Rows:** 1,361
- **Source:** [U.S. Bureau of Labor Statistics](https://www.bls.gov/cpi/)
- **Licence:** US federal government work, public domain.
- **Refresh:** Re-baked when BLS publishes annual averages

### `us-cpi-by-category.csv`

Monthly CPI index for each of the nine major expenditure groups, back to 1990.

- **Columns:** `category, label, bls_series, month, index_value`
- **Rows:** 3,870
- **Source:** [U.S. Bureau of Labor Statistics](https://www.bls.gov/cpi/)
- **Licence:** US federal government work, public domain.
- **Refresh:** Re-baked when BLS publishes annual averages

### `ecb-fx-daily.csv`

Daily euro reference rates converted to each tracked currency pair.

- **Columns:** `date, pair, rate`
- **Rows:** 10,360
- **Source:** [European Central Bank, via Frankfurter](https://www.frankfurter.dev/)
- **Licence:** ECB reference rates are freely reusable with attribution.
- **Refresh:** Re-baked periodically; ECB publishes each business day

### `ecb-fx-latest.csv`

The most recent euro reference rate for every currency the ECB publishes.

- **Columns:** `currency, rate, base, date`
- **Rows:** 30
- **Source:** [European Central Bank, via Frankfurter](https://www.frankfurter.dev/)
- **Licence:** ECB reference rates are freely reusable with attribution.
- **Refresh:** Re-baked periodically; ECB publishes each business day

### `us-recession-indicators.csv`

Five recession indicators as a long series: Sahm Rule, yield curve, recession probability, Chicago Fed activity and jobless claims.

- **Columns:** `date, indicator, indicator_name, value, threshold`
- **Rows:** 1,594
- **Source:** [Federal Reserve Bank of St. Louis (FRED)](https://fred.stlouisfed.org/)
- **Licence:** Underlying series are public domain. Not endorsed or certified by the Federal Reserve Bank of St. Louis.
- **Refresh:** Re-baked periodically

### `us-national-debt.csv`

Total public debt outstanding, from the Treasury "Debt to the Penny" dataset.

- **Columns:** `date, total_debt_usd`
- **Rows:** 259
- **Source:** [U.S. Department of the Treasury](https://fiscaldata.treasury.gov/datasets/debt-to-the-penny/)
- **Licence:** US federal government work, public domain.
- **Refresh:** Re-baked periodically; Treasury publishes each business day

### `us-mortgage-rate-30y.csv`

The Freddie Mac Primary Mortgage Market Survey 30-year fixed rate.

- **Columns:** `date, rate_pct`
- **Rows:** 146
- **Source:** [Freddie Mac PMMS, via FRED](https://fred.stlouisfed.org/series/MORTGAGE30US)
- **Licence:** Retrieved from FRED as a public-domain series. Not endorsed or certified by the Federal Reserve Bank of St. Louis.
- **Refresh:** Every Monday, 06:17 UTC

### `us-i-bond-rates.csv`

Every I bond rate period since 1998, with the fixed and inflation components split out.

- **Columns:** `period_from, period_to, fixed_rate, inflation_rate`
- **Rows:** 57
- **Source:** [U.S. Department of the Treasury, TreasuryDirect](https://www.treasurydirect.gov/savings-bonds/i-bonds/i-bonds-interest-rates/)
- **Licence:** US federal government work, public domain.
- **Refresh:** Re-baked each May and November reset

### `central-bank-policy-rates.csv`

Current headline policy rate for each tracked central bank.

- **Columns:** `bank, country, currency, rate_name, rate_pct, as_of`
- **Rows:** 5
- **Source:** [Each central bank, published directly](https://www.ecb.europa.eu/)
- **Licence:** Each source was licence-checked to permit redistribution with attribution.
- **Refresh:** Re-baked periodically and after policy meetings

### `economic-calendar.csv`

Scheduled statistical releases and central bank decisions, from official published calendars.

- **Columns:** `date, time_utc, title, country, impact`
- **Rows:** 232
- **Source:** [National statistics agencies and central banks](https://fred.stlouisfed.org/)
- **Licence:** Official published release schedules, public domain or open licence.
- **Refresh:** Every Monday, 06:17 UTC

### `euro-area-calendar.csv`

Headline euro-area statistical releases from the Eurostat calendar.

- **Columns:** `date, time_utc, title, country, impact`
- **Rows:** 15
- **Source:** [Eurostat](https://ec.europa.eu/eurostat/)
- **Licence:** Eurostat data is reusable with attribution.
- **Refresh:** Every Monday, 06:17 UTC

### `earnings-date-estimates.csv`

Estimated reporting windows derived from each company’s own SEC filing cadence. Estimates, not confirmed dates.

- **Columns:** `date, symbol, title, country, impact, basis`
- **Rows:** 85
- **Source:** [SEC EDGAR filing history (our derivation)](https://www.sec.gov/edgar)
- **Licence:** Derived by us from public SEC filings. Estimates, not confirmed company guidance.
- **Refresh:** Every Monday, 06:17 UTC

### `crypto-staking-yields.csv`

Nominal and real staking yield per protocol, computed from each protocol’s own issuance formula.

- **Columns:** `coin, name, symbol, nominal_apy, inflation_rate, real_yield, source`
- **Rows:** 4
- **Source:** [Protocol issuance formulas applied to live on-chain totals (our computation)](https://ethereum.org/en/staking/)
- **Licence:** Computed by us from public on-chain data, not resold from a staking-data vendor.
- **Refresh:** Re-baked periodically

### `irs-rmd-uniform-lifetime-table.csv`

The distribution period factor for each age, used to compute required minimum distributions.

- **Columns:** `age, distribution_period`
- **Rows:** 48
- **Source:** [Internal Revenue Service, Publication 590-B, Appendix B, Table III](https://www.irs.gov/publications/p590b)
- **Licence:** US federal government work, public domain.
- **Refresh:** Re-baked when the IRS revises the table

### `nber-recessions.csv`

Every NBER-dated US recession back to 1854, with start month, end month and length.

- **Columns:** `start_month, end_month, length_months, left_censored`
- **Rows:** 35
- **Source:** [NBER recession dates via FRED (USREC)](https://fred.stlouisfed.org/series/USREC)
- **Licence:** US public-domain series. Not endorsed or certified by the Federal Reserve Bank of St. Louis.
- **Refresh:** Re-baked periodically; the NBER dates recessions in hindsight

### `bitcoin-halvings.csv`

Every halving to date with its block height, date and the block reward that followed.

- **Columns:** `block, date, reward_after_btc, label`
- **Rows:** 5
- **Source:** [Bitcoin blockchain, via mempool.space](https://mempool.space/)
- **Licence:** Block heights and rewards are public blockchain facts.
- **Refresh:** Re-baked periodically

## Where these come from

Economicium is a set of free tools for trading and personal finance built on
official public data. Every calculator shows its formula and every data tool
names its source. Full sourcing and refresh cadence for everything:
<https://economicium.com/methodology/>
