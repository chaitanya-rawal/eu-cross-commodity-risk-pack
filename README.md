# European Cross-Commodity Risk Pack
**Author:** Chaitanya Rawal  
**Email:** chaitanya.rawal0804@gmail.com

## Overview
Automated monitor that converts European gas and carbon fundamentals 
into a repeatable trading narrative for European power markets 
(Day-Ahead to curve).

## How to Run
```bash
python risk_pack.py
```

## Output Files
| File | Description |
|---|---|
| risk_pack_output.docx | Auto-generated desk note with metrics, narrative, charts |
| chart1_ttf_eua.png | TTF Gas vs EUA Carbon — 90 day view |
| chart2_power_cds.png | DE Day-Ahead Power + Clean Dark Spread |
| ai_log.txt | Logged AI prompts and outputs |

## Data Sources
| Data | Source |
|---|---|
| TTF Gas | FRED API |
| EUA Carbon | Stooq |
| EU Gas Storage | GIE AGSI+ |
| DE Day-Ahead Power | Energy-Charts.info |
| AI Narrative | Anthropic Claude API |

## Monitor Metrics
| Metric | Unit | Trading Relevance |
|---|---|---|
| TTF Front Month | $/MMBtu | Prompt gas benchmark |
| TTF EUR Equivalent | €/MWh | Gas cost into power stack |
| EUA Price | €/tCO2 | Carbon cost input |
| EUA 30d Momentum | % | Policy and supply signal |
| EU Gas Storage | % full | Structural gas buffer |
| Storage vs 5yr Avg | pp | Relative tightness signal |
| DE Day-Ahead Power | €/MWh | Realised power benchmark |
| Clean Dark Spread | €/MWh | Gas to power profitability |
| Power-Carbon Correlation | r | Cross-commodity regime |

## Clean Dark Spread Formula
```
CDS = DA_Power - (TTF_EUR_MWh / Heat_Rate) - (EUA_Price x Emission_Factor)
Heat Rate       = 0.45 (CCGT efficiency)
Emission Factor = 0.34 tCO2/MWh
```

## Dependencies
```bash
pip install pandas numpy matplotlib seaborn requests
pip install python-docx fredapi anthropic certifi urllib3
```

## AI Integration
Script feeds live metrics into Claude API with a structured prompt.
Claude writes a 3-paragraph morning desk note as a senior European 
energy trader. All prompts and outputs are logged to ai_log.txt 
with timestamps for full auditability.

## Architecture
```
risk_pack.py
├── Section 1: Data Pull (FRED, Stooq, GIE, Energy-Charts)
├── Section 2: Metric Computation (CDS, correlations, momentum)
├── Section 3: Chart Generation (matplotlib)
├── Section 4: AI Narrative (Claude API + logging)
└── Section 5: Word Document Assembly
```