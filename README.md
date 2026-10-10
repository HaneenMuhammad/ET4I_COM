# ET4I-COM Code: Adaptive Evapotranspiration Estimation Using Satellite and Reanalysis Products

Code for: Muhammad et al. (2026). *An adaptive method to estimate evapotranspiration using satellite and reanalysis products.* Hydrology and Earth System Sciences.

Evaluates 10 remote evapotranspiration (ET) products against Penman–Monteith (PM) ET at 21 Irish stations (2018–2023, 8-day steps), and improves them using Adaptive Bias correction (AB) and a dynamic weighted combination (COM), compared with Simple Taylor Skill fusion (STS; [Yao et al., 2017](https://doi.org/10.1016/j.jhydrol.2017.08.013)).

## Structure

```
DATA/        input data (included) and all .nc outputs
CODE/        ET4I_*.ipynb and taylorDiagram.py
```

## Input data

```
DATA/
├── Stations.txt        station codes, one per line (e.g. AY)
├── Stations.csv        columns: station_name, StationCode, lat, lon (decimal degrees)
├── Products.txt        product names, one per line (PM must be first)
├── AY/
│   ├── PM_AY.nc
│   ├── AQUA_AY.nc
│   └── ...             one file per product: <PRODUCT>_<STN>.nc
├── BE/
└── ...                 one folder per station
```

Each `.nc` file holds one variable, `ET` (mm/8-days), for one product at one station, with dimensions `(DOY, Year)`: `DOY` = 1, 9, 17, …, 361 (46 periods) and `Year` = 2018–2023.

## Notebooks

Listed in the order their results appear in the paper. Running them in this order also satisfies all data dependencies.

1. `ET4I_DATA` – builds the dataset and error statistics
2. `ET4I_Spatial` – station map
3. `ET4I_AdaptiveBias` – AB correction
4. `ET4I_COM` – COM fusion
5. `ET4I_doy_combined` – seasonal cycle
6. `ET4I_Taylor_Original` – Taylor diagram, raw products
7. `ET4I_Taylor_AB` – Taylor diagram, raw vs AB
8. `ET4I_COUNT` – best product frequency
9. `ET4I_STS` – STS benchmark
10. `ET4I_Taylor_LSA_COM_STS` – Taylor diagram, LSA vs COM vs STS
11. `ET4I_ET_ERR_TimeSeries` – error time series
12. `ET4I_Seasonal` – seasonal comparison
13. `ET4I_Resolution` – RMSE vs resolution
14. `ET4I_Coastal_Inland` – coastal vs inland

## Notes

- `taylorDiagram.py` by Yannick Copin, *Taylor diagram for python/matplotlib*, https://doi.org/10.5281/zenodo.5548061
- The input files include an additional ET estimate (TH), which is not used in this study and is excluded from all analyses.
