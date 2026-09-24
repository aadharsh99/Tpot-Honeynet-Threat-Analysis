# Data

The submitted project report contains analysed T-Pot telemetry but does not include the original raw dataset or exported Elasticsearch/Cowrie/Honeytrap records.

This directory is intentionally kept free of reconstructed or invented raw data.

If the original dataset becomes available, recommended organisation is:

```text
data/
├── raw/
│   ├── cowrie/
│   ├── honeytrap/
│   └── tpot/
├── processed/
└── README.md
```

Document the collection period, timezone, field definitions and any anonymisation performed before committing telemetry.
