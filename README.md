# SPC Weekly Report Automation

**Automated Statistical Process Control (SPC) analysis and reporting system for key business metrics.**

## 🎯 Purpose

Fully automate the weekly reporting process that analysts currently do manually:

- ✅ Apply Statistical Process Control analysis to key metrics weekly
- ✅ Detect process stability (improving, deteriorating, or special-cause signals)
- ✅ Generate natural-language commentary explaining what the numbers mean
- ✅ Create clean, readable XmR control charts
- ✅ Package everything into Slack-ready reports

## 🚀 Quick Start

### Prerequisites

```bash
# Python 3.10+
pip install -r requirements.txt

# Google Cloud authentication
gcloud auth application-default login
```

### Usage

```python
from spc_analysis import SPCConfig, run_spc_analysis

# 1. Configure for your data
config = SPCConfig(
    metric_column='measure',        # Column to group by
    value_column='value',           # Numeric values
    date_column='partition_date',   # Date column
    
    metric_labels={                 # Optional: friendly names
        'my_metric': 'My Metric Name',
    },
)

# 2. Run analysis
output = run_spc_analysis(df, config)

# 3. Get outputs
results = output['results']       # Raw data with anomaly flags
figures = output['figures']       # XmR charts
commentary = output['commentary'] # Report generator

# 4. Generate Slack message
summaries = commentary.generate_all_summaries()
slack_message = commentary.format_slack_message(summaries)
```

## 📊 Western Electric Rules

The system detects these SPC signals:

| Rule | Name | Description |
|------|------|-------------|
| R1 | Beyond 3σ | Single point outside control limits (critical) |
| R2 | 2/3 >2σ | 2 of 3 consecutive points beyond 2σ |
| R3 | 4/5 >1σ | 4 of 5 consecutive points beyond 1σ |
| R4 | 8 same side | 8 consecutive points on same side of mean |
| R5 | 6 trending | 6 consecutive points trending same direction |
| MR | Volatility | Moving Range exceeds Upper Control Limit |

## 🔧 Configuration

All settings are centralized in `SPCConfig`:

```python
@dataclass
class SPCConfig:
    # Required: Data column mappings
    metric_column: str = 'measure'
    value_column: str = 'value'
    date_column: str = 'partition_date'
    
    # Optional: Analysis parameters
    rules_active: List[int] = [1, 2, 3, 4, 5]
    min_data_points: int = 10
    
    # Optional: Report customization
    report_title: str = "Weekly SPC Report"
    team_name: str = "SPC Analysis System"
    
    # Optional: LLM settings (for executive summaries)
    llm_provider: str = 'anthropic'  # or 'openai'
    llm_model: str = 'claude-sonnet-4-20250514'
    
    # Optional: Brand colors
    colors: Dict[str, str] = {...}
```

## 📁 Project Structure

```
├── Untitled0.ipynb      # Main analysis notebook
├── README.md            # This file
├── requirements.txt     # Python dependencies
├── style_guide.txt      # Brand styling reference
└── .gitignore
```

## 🔮 Future Enhancements

- [ ] Slack API integration for automated posting
- [ ] Cloud Functions deployment for weekly scheduling
- [ ] Historical comparison (week-over-week)
- [ ] Additional chart types (CUSUM, EWMA)

## 📝 License

Internal use only — Soundtrack Your Brand

---

*Built during Hackweek 2026*
