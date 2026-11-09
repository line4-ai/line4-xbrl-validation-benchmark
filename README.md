# Line4 XBRL validation benchmark

Results of benchmarking the Line4 XBRL validation engine against [Arelle](https://arelle.org), the widely used open-source reference processor, on about 290 sample filings across recent EBA, EIOPA and ESEF releases (November 2026).

Full write-up, including the caveats: https://www.line4.ai/blog/xbrl-validation-engine-benchmark

## Headline results

| Measure | Result |
| --- | --- |
| Agreement with Arelle, formula assertions | 99.95% (417,342 of 417,531) |
| Agreement on EBA reporting frameworks 4.0 to 4.3 | 100% (330,046 assertions, plus instance, DTS and validation-code checks) |
| One large FINREP filing, controlled conditions | 16 seconds, against 4.2 hours for Arelle |

## By release

| Release | Agreement | Detail |
| --- | --- | --- |
| EBA 4.0, 4.1, 4.2, 4.3 | 100% | 330,046 assertions, plus every instance, DTS and validation-code comparison |
| EIOPA Solvency II, pension funds, IRRD, FICOD | 99.84% | 86,824 of 86,960 assertions |
| ESEF | 98.1% | 472 of 481 assertions, plus a few document and context differences |

## Data

- `results/agreement-by-release.csv`: agreement with the reference processor, by release family
- `results/speed.csv`: validation times, with conditions and caveats

## Method

- About 290 sample filings across every release the engine supports.
- For each filing, every formula assertion result was compared with Arelle's. For the EBA releases, every instance, DTS and validation-code outcome was compared as well.
- Each run makes the engine better: every disagreement is investigated, what we learn goes into the next iteration with a test to lock it in, and where the reference engine is the one that differs, we write it up.

## The disagreements

About 190 assertions disagree, from a handful of causes repeated across filings:

- One EIOPA Solvency II assertion disagrees in all three releases.
- A few other EIOPA assertions produce different counts.
- Around a dozen agree on the counts but bind different facts. That can be a real difference or a difference in how facts are keyed.
- ESEF shows a few classification and context-count differences.

## Speed, with the caveats

On one large FINREP filing, measured under controlled conditions, the Line4 engine took 16 seconds against Arelle's 4.2 hours. Across the full set, a first run suggests around 160 times faster: Arelle's recorded time adds up to 35.8 hours of CPU, against 13.5 minutes for the Line4 engine. Treat that wider figure as rough. Both ran on a heavily loaded machine and Arelle is single-threaded. A controlled head-to-head is still to come, and we will publish it here.

## Questions to ask any XBRL validation engine

1. How closely does it agree with a reference implementation, release by release, and where does it differ?
2. Who investigates each disagreement, and how quickly is it fixed or explained?
3. How long does it take to validate your largest return, measured under controlled conditions?
4. How long would it take to re-validate a year of filings after a rule change?
5. Can your team change and version the rules, or does every change wait for a release?

## About Line4

[Line4](https://www.line4.ai) builds modern SupTech for financial regulators: regulatory data collection, validation, AI review of returns and casework, deployed by engineers inside the regulator's team.

Figures are from Line4's internal benchmark, November 2026. Arelle is an open-source XBRL processor; we used it as the reference because it is widely used and freely available for anyone to check our numbers.

## Licence and citation

Results and text: CC BY 4.0 (see `LICENSE`). Citation details: `CITATION.cff`.
