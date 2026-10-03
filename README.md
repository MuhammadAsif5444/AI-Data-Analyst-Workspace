# Data Analyst Workspace

Upload a CSV, ask a business question in plain English, and get an answer backed by the data.

Most people who need numbers from a spreadsheet don't want to write formulas or SQL. They want to ask "what's driving revenue?" and get a straight answer. This project does that: an AI agent reads your data, works out how to answer the question, and returns the findings with supporting analysis.

---

## What it does

- **Takes one or more CSV files.** Related files (for example, orders and customers) can be uploaded together, and the agent can combine them.
- **Answers business questions in plain language.** No query syntax needed.
- **Runs the analysis on its own.** The agent decides what to look at, so you don't have to specify steps.
- **Handles larger files through Google Cloud Storage.** Files over 1 MB can't be uploaded inline, so you paste a GCS URI instead.

## How it works

1. **Choose a dataset.** Drop in your CSV file(s) or click to browse. Each file must be 1 MB or smaller. For anything bigger, paste a GCS URI and use **Add GCS File**.
2. **Ask a business question.** Type your own, or start with one of the built-in prompts.
3. **Click Analyze.** The agent works through the data and reports back.

### Starter questions

These are good for a first run, and they work on almost any dataset:

- *Summarize the key trends and the most important drivers in this data.*
- *What are the top segments by value, and how do they differ?*
- *Are there any anomalies or outliers I should investigate?*

## Getting started

> **Note:** Fill in the setup details below to match your own environment. They are left as placeholders on purpose.

### Prerequisites

- `<runtime and version, e.g. Python 3.11 or Node 20>`
- `<API key or credentials for the model provider>`
- A Google Cloud project with a storage bucket, only if you plan to use the GCS option

### Installation

```bash
git clone <your-repo-url>
cd <your-project-folder>
<install command>
```

### Configuration

Create a `.env` file in the project root:

```
API_KEY=your_key_here
GCS_BUCKET=your_bucket_name   # optional, needed for files over 1 MB
```

### Running locally

```bash
<start command>
```

Then open the app in your browser at `<local address>`.

## Try it with the sample data

The `test-data/` folder has two CSV files built to exercise the app. They contain known patterns, so you can check whether the agent finds them.

| File | Contents |
|---|---|
| `test_orders.csv` | 3,001 sales orders from 2024 to 2025 (revenue, cost, product, channel, discount) |
| `test_customers.csv` | 300 customers with region, tier, and signup date. It joins to orders on `customer_id`. |

Upload both together to test the multi-file flow.

### What the agent should find

**Trends and drivers**
- Revenue grows steadily, around 1.5% a month.
- November and December are noticeably stronger than other months.
- Enterprise customers and North America bring in the most revenue.

**Segments**
- Revenue ranks Enterprise > Mid-Market > SMB.
- Hardware margins (about 30%) are well below Software and Services (about 45%).

**Anomalies**
- One order with revenue about 40 times the normal amount.
- One order with a quantity of 900.
- One order with negative revenue.
- One order where cost is three times revenue.
- A run of 31 orders with an unusual 60% discount.
- A cluster of 11 very large Direct Sales deals.

**Data quality issues**
- 25 missing `channel` values and 15 missing `discount` values.
- One duplicated order row.

If the agent reports these without being told where to look, the pipeline is working.

## Project structure

```
.
├── README.md
├── test-data/
│   ├── test_orders.csv
│   └── test_customers.csv
└── <your source folders>
```

## Limitations

- Inline uploads are capped at 1 MB per file.
- Results come from an AI model, so check important numbers before acting on them. The agent can misread a column, make assumptions about messy data, or state a conclusion more confidently than the data supports.
- Quality depends on the data. Clear column names and clean values give better answers.

## Data and privacy

Don't upload data you don't have the rights to use, and avoid sensitive personal information unless you're sure it is allowed. Uploaded content is processed by Google's generative AI services, and your use is subject to the applicable [Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) and [terms](https://ai.google.dev/gemini-api/terms). Don't use the tool to generate content that infringes on others' intellectual property or privacy rights.

## Contributing

Bug reports and pull requests are welcome. For larger changes, open an issue first so we can talk through the approach.

## License

`<add your license here>`