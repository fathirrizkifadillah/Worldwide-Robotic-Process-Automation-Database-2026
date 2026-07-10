# Worldwide Robotic Process Automation Database 2026

Exploratory data analysis and ROI modelling on the synthetic Kaggle dataset **Worldwide Robotic Process Automation Database 2026**.

## Scope and limitations

- This is a synthetic dataset. Results are illustrative and must not be interpreted as facts about named companies, industries, platforms, or the global RPA market.
- The data-quality checks identify intentional synthetic artifacts, including market shares that sum to more than 100% and deployment dates that can precede their project start dates.
- EDA findings describe associations in this dataset only; they do not establish causality.

## Run locally

```bash
python -m venv .venv
.venv\\Scripts\\activate
pip install -r requirements.txt
jupyter notebook main.ipynb
```

The notebook downloads the source through `kagglehub`. Record the downloaded dataset version and run date when reproducing results.

## Models

- **Model 1** is a leakage demonstration: it includes realized financial features and illustrates why near-perfect ROI prediction is not a valid forecast.
- **Model 2** is the strict pre-planning model. It uses only budget, planned robot count, timing, and proposed categorical project attributes. It excludes realized savings, employee hours saved, savings-derived ratios, and project status.

Evaluate Model 2 against the median baseline and its printed 5-fold cross-validation results. It is a benchmark for synthetic data, not a production decision system.
