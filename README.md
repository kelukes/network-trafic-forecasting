# Network Traffic Peak Forecasting for ISP Capacity Planning


## Problem
Forecast the **daily 95th percentile of uplink traffic** (bps) 
for a 14-day horizon using real infrastructure monitoring data 
from cloud provider exported from Zabbix).

## Dataset
- Hourly uplink traffic data: 2025-08-19 → 2026-04-05
- Resampled to daily p95 series: 230 observations
- Raw data is proprietary and not included in this repo

## Models tested
| Model | RMSE |
|---|---|
| Random Forest (recursive) | 145M bps |
| Seasonal Naïve (t-7) | 162M bps |
| SARIMA(0,1,2)(1,0,0,7) | 167M bps |
| Prophet (changepoint_prior=0.01) | ~250M bps |
| Ridge (recursive) | 297M bps |

## Key findings
- Seasonal Naïve outperformed all statistical models (ARIMA/SARIMA/Prophet)
- Random Forest with lag/rolling/calendar features beat all baselines
- Prophet's default trend overfit to spike events; regularisation improved but did not close the gap
- Spike events (kurtosis = 27.89) are not reliably forecast by any tested model

## Structure
- `notebooks/` — main analysis notebook (sections 0–10)
- `outputs/` — RF 14-day forecast CSV
- `docs/` — dataset documentation

## Requirements
```bash
pip install -r requirements.txt
```


Capstone project — Applied AI/ML, Tomorrow University
