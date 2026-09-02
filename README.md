# US Lottery Tax Data

**Open dataset, CC0-licensed** — free to copy, redistribute, remix, and cite, no attribution required. How much of a US Powerball / Mega Millions jackpot a winner actually keeps, broken down by 51 countries of residence.

This is the raw data behind [chamtax.com](https://chamtax.com), a US lottery tax calculator that supports 51 residency profiles and 36 languages. See also the [full public dataset hub](https://chamtax.com/lottery-tax-data-hub.html) (this dataset plus a companion US state-by-state tax rate dataset, both as CSV/JSON) and the [Kaggle mirror](https://www.kaggle.com/datasets/chamtax/us-lottery-jackpot-tax-by-country).

## Why this exists

Winning a US lottery jackpot triggers a flat 30% US federal withholding for non-resident aliens ([IRC §871(a)](https://www.law.cornell.edu/uscode/text/26/871)), unless a tax treaty reduces it. What happens *after* that depends entirely on the winner's country of tax residence — some countries offset the US withholding with a Foreign Tax Credit and charge nothing more, others add a further national tax on top. That second number is scattered across dozens of tax authority websites, treaty texts, and outdated blog posts. This repo collects it in one place.

## Files

- **`data.json`** — full dataset with methodology, confidence levels, and per-country detail page links
- **`data.csv`** — same data, flattened for spreadsheets / pandas

## Methodology

Every row is generated directly from the same tax engine that runs [chamtax.com](https://chamtax.com) (`calcTakeHome()`), not hand-transcribed — so the numbers here match what the live calculator shows. Effective percentages are computed for a large lump-sum jackpot scenario (~$100M USD) to reflect realistic progressive-bracket behavior where applicable. Eight countries (Netherlands, Russia, Laos, Indonesia, Uzbekistan, Kyrgyzstan, Myanmar, Switzerland) apply zero Foreign Tax Credit in the engine — their home-country tax stacks fully on top of the 30% US withholding instead of being offset by it; this is called out explicitly in each of those rows' `homeCountryTax` field. Two countries (United Arab Emirates, Saudi Arabia) have no personal income tax at all, so there's no FTC question — nothing is owed beyond the US withholding. Ukraine's residual is a partial-FTC case: the treaty credit covers its 18% personal income tax but not the separate 5% military levy.

## Confidence levels

Not all 51 countries have equally solid sourcing. Every row is labeled:

| Level | Meaning |
|---|---|
| `verified` | Based on an identifiable statute, treaty article, or official tax authority guidance |
| `verified_treaty_suspended` | Based on statute/treaty, but the underlying tax treaty is currently suspended (e.g. Russia) |
| `approximate` | Reasonable approximation from secondary sources, not a primary legal citation |
| `unverified_estimate` | No authoritative source found — best-effort estimate, don't rely on it for filing |

**This is not tax advice.** Rates change, treaties get renegotiated, and estimates can be wrong. If you're an actual winner (congratulations), talk to a tax professional in your country. If you know of a mistake or an authoritative source for an `unverified_estimate` row, please open an issue — corrections are very welcome and will be reflected on chamtax.com too.

## Live calculator

For an interactive version — including US state-level breakdowns, annuity-vs-lump-sum comparison, and 36 languages — see **[chamtax.com](https://chamtax.com)**.

## License

Data in this repository (`data.json`, `data.csv`) is released under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) — use it however you like, attribution appreciated but not required.
