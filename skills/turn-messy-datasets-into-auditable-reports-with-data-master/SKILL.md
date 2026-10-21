---
name: "Turn messy datasets into auditable reports with data-master"
slug: "turn-messy-datasets-into-auditable-reports-with-data-master"
description: "Use data-master to preserve raw tabular data, hold ambiguous cleaning decisions for review, run unit-aware statistics and sensitivity checks, and produce Markdown, HTML and PDF reports with machine-verifiable audit evidence."
verification: "listed"
source: "https://github.com/MAGA2010/data-master"
author: "MAGA2010"
publisher_type: "individual"
category: "Data Extraction & Transformation"
framework: "Codex"
---

# Turn messy datasets into auditable reports with data-master

Use data-master when a CSV, TSV, Excel, JSON, JSONL or Parquet analysis must be
reproducible and reviewable rather than a one-off notebook. The tool reads
potentially destructive fields as text first, records every cleaning decision,
and refuses to guess when values could have more than one valid meaning, such as
zero-padded identifiers or compact values that could be dates or integers. It
supports declared independent units, repeated measures, paired comparisons,
covariate-adjusted comparisons, sensitivity analysis and descriptive time-series
work. A completed run includes cleaned data, a replayable cleaning program,
machine-readable statistics, charts, Markdown, self-contained HTML, PDF and a
separate audit verdict. Use the saved verification command before relying on a
delivered report. Treat unresolved holds and failed audit gates as questions for
the dataset owner; do not silently replace them with weaker assumptions.

## Installation

Requires Python 3.11 or newer. The GitHub npm launcher also requires Node.js 20
or newer and does not run installation hooks.

```bash
npm install -g github:MAGA2010/data-master#v0.3.0
data-master setup
data-master doctor
data-master skill install
```

To install from Python source instead:

```bash
git clone --branch v0.3.0 --depth 1 https://github.com/MAGA2010/data-master.git
cd data-master
python -m pip install .
data-master doctor
data-master skill install
```

`data-master skill install` registers the bundled skill in the Codex skills directory
(`$CODEX_HOME/skills/data-master`, or `~/.codex/skills/data-master` by default).
Restart Codex after installation so it discovers the skill. The installer refuses
to overwrite an existing copy; use `--target <directory>` for a separate install.

Run the bundled synthetic demonstration, then inspect both the report and audit:

```bash
data-master demo --out outputs/first-demo
data-master verify outputs/first-demo --json
```

Analyze supplied data by declaring the grouping, independent-unit and outcome
columns when they are known:

```bash
data-master analyze measurements.csv --out outputs/study \
  --group treatment --unit-key participant_id \
  --outcomes response_time,accuracy
```

If the run writes `answers.template.json`, obtain the missing study or cleaning
decision from the user, fill the template using its stable decision IDs, and save
the completed file as `outputs/study/answers.json`. Resume the saved run with:

```bash
data-master resume outputs/study/state.json --answers outputs/study/answers.json
```

## Documentation

Reviewed release: `v0.3.0`, commit
[`9d22e2505071424d7e41dc2ee5b875b45a1ed574`](https://github.com/MAGA2010/data-master/tree/9d22e2505071424d7e41dc2ee5b875b45a1ed574).

- [Source and quick start](https://github.com/MAGA2010/data-master)
- [Evaluation evidence](https://github.com/MAGA2010/data-master/blob/9d22e2505071424d7e41dc2ee5b875b45a1ed574/EVALUATION.md)
- [Validation matrix](https://github.com/MAGA2010/data-master/blob/9d22e2505071424d7e41dc2ee5b875b45a1ed574/docs/VALIDATION.md)
- [Agent Skill Exchange](https://agentskillexchange.com/skills/turn-messy-datasets-into-auditable-reports-with-data-master/)
