# Bike-sharing and Public Transport: Accessibility and Equity in Luxembourg

This study examines first mile, last mile and combined station based e-bike integration with public transport (PT) across Luxembourg. It uses gravity based measures from 1 km population grid cells to eight categories of opportunities. Population weighted Theil indices are then used to examine equity in accessibility levels and in the incremental gains from integration, decomposing by municipality, nationality and socio-economic status.


## Repository structure

```
├── gravity/
│   ├── build_graphs.ipynb                       
│   ├── create_pt_times_via_r5py.ipynb           
│   ├── compute_gravity.ipynb                    
│   ├── compute_station_proximity_network.ipynb  
│   ├── requirements.txt
│   ├── data/                                    # input data (not included)
│   └── cache/                                   # generated graphs (not included)
│
└── theil_index/
    ├── create_grid_to_municipality.ipynb        
    ├── compute_theil.ipynb                      
    ├── requirements.txt
    └── data/                                    # input data (not included)
```

## Installation

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r gravity/requirements.txt
pip install -r theil_index/requirements.txt
```

`create_pt_times_via_r5py.ipynb` also needs **Java JDK 21** (required by r5py), installed separately.

## Data

The input data are not included in this repository because of their size. The cleaned datasets are available from the author on request. Place the following files in the `data/` folders:

**`gravity/data/`**

| File | Content |
|---|---|
| `EU_DEM_Lux.tif` | Digital elevation model (EU-DEM), clipped to Luxembourg |
| `luxembourg-260310.osm.pbf` | OpenStreetMap extract for r5py |
| `gtfs.zip`, `gtfs/stops.txt` | Luxembourg GTFS feed |
| `stops_only_luxemburg.csv` | PT stops within Luxembourg |
| `bike_stations_merged.csv` | Bike-sharing station locations |
| `origins.csv` | 1 km population grid |
| `pois.csv` | Opportunities in eight categories |

**`theil_index/data/`**

| File | Content |
|---|---|
| `origins.csv` | 1 km population grid |
| `lux_census_2021_socio.csv` | 2021 census, population by nationality |
| `indice_socio_economique_communes.csv` | Socio-economic index per municipality |
| `limadmin-shp/LIMADM_COMMUNES.shp` | Municipality boundaries |
| `accessibility_results_sigma_20p0.csv` | Output of `compute_gravity.ipynb` |

## How to run

Run the notebooks in this order, each from its own folder:

1. `gravity/build_graphs.ipynb`: downloads the OSM network 
2. `gravity/create_pt_times_via_r5py.ipynb`
3. `gravity/compute_gravity.ipynb`, then copy `accessibility_results_sigma_20p0.csv` to `theil_index/data/`
4. `theil_index/create_grid_to_municipality.ipynb`
5. `theil_index/compute_theil.ipynb`

