# 🚲 Montreal Réseau Express Vélo (REV) Optimization

**A Three-Phase Optimization Framework for Corridor Discovery, Budget Allocation, and Construction Sequencing**

## 📋 Project Overview

Montreal's Réseau Express Vélo (REV) is an ambitious network of protected cycling corridors designed to transform urban mobility. Despite a $214M budget and plans for 184 km of infrastructure, only 24 km have been completed, leaving the network fragmented and underutilized.

This project develops a **data-driven, optimization-based framework** to guide REV expansion by answering a critical question: *How should Montreal prioritize and sequence REV corridor construction to maximize mobility impact under real-world constraints?*

Using spatial clustering, integer linear programming, and construction scheduling optimization, we identify an optimal set of corridors that maximizes accessibility, reduces fragmentation, and accelerates meaningful network connectivity.

## 🎯 Key Results

- **8 optimal corridors** selected spanning **93.88 km**
- **1.38 million annual BIXI trips** captured
- **$184.77M** budget utilization (99.3% of available $186M)
- **5-year construction timeline** (20 quarters) with 5 concurrent teams
- **Seasonal productivity adjustments**: Summer +20%, Winter -40%

## 🏗️ Three-Phase Methodology

### Phase 1: Corridor Discovery
- Processed **8,899 candidate street segments** from GeoPack files
- Removed 441 segments overlapping existing REV infrastructure
- Applied **DBSCAN clustering** and linear path extraction to identify continuous, navigable corridors
- Implemented edge-tracking mechanisms to prevent circular path formation
- Retained only corridors ≥3 km for meaningful network contribution

### Phase 2: Corridor Selection (Integer Linear Programming)
- **Objective**: Maximize total BIXI trip demand
- **Constraints**: Budget ($186M), maximum 8 corridors, non-overlapping segments
- **Solver**: Gurobi optimization
- Selected 8 high-impact corridors balancing demand, cost, and geographic coverage

### Phase 3: Construction Scheduling (Mixed-Integer Programming)
- **Objective**: Minimize project duration and team count
- **Constraints**: Maximum 2 new projects per quarter, seasonal productivity variations, team availability
- **Result**: 20-quarter (5-year) schedule using 5 teams
- Identified Corridor 21 (47.1 km) as critical path

## 📊 Sensitivity Analysis

| Parameter | Range Tested | Key Insight |
|-----------|--------------|-------------|
| Budget | $100M–$250M | $186M is optimal; diminishing returns beyond |
| Demand | -30% to +50% | Selected corridors remain stable across scenarios |
| Teams | 3–7 | 5 teams optimal; adding beyond yields minimal gain |
| Winter Penalty | -20% to -60% | Reducing penalty from -40% to -30% saves 1 year |
| Start Limits | 1–4 per quarter | 2 starts/quarter optimal |

## 🗂️ Repository Structure

```
Montreal_REV_Optimization/
│
├── data/
│   ├── raw/                      # Original data sources
│   │   ├── reseau-express-velo.geojson
│   │   └── montreal_bike_network.gpkg
│   ├── datasets for optimization/ # Processed datasets
│   │   ├── BIXI_Demand_with_Segment_Data_Integration.ipynb
│   │   ├── Canstats_OSM_REV_Data_Integration.ipynb
│   │   ├── montreal_rev_optimization.gpkg
│   │   └── rev_connector_candidates.csv
│   └── processed/                 # Cleaned intermediate data
│
├── dataset_EDA/                   # Exploratory visualizations
│   ├── bixi_demand_analysis.png
│   ├── connectivity_analysis.png
│   ├── top_20_demand_corridors.png
│   └── ...
│
├── final_code/
│   └── Final Code.ipynb           # Main optimization notebook
│
├── results/                        # Output visualizations
│   ├── Montreal_REV_Corridor_Map.png
│   ├── rev_construction_timeline.png
│   ├── team_assignments_timeline.png
│   ├── sensitivity_teams_vs_makespan.png
│   └── ...
│
├── report/
│   └── Final Written Report.docx   # Complete project documentation
│
└── README.md
```

## 🛠️ Technologies Used

- **Spatial Analysis**: GeoPandas, Shapely, Fiona, DBSCAN (scikit-learn)
- **Optimization**: Gurobi (ILP & MIP)
- **Data Processing**: Python, Pandas, NumPy
- **Visualization**: Matplotlib, Seaborn, Contextily
- **Data Formats**: GeoPackages, GeoJSON, Shapefiles
- **Version Control**: Git

## 📈 Key Visualizations --> results

## 🔍 Key Findings

1. **Budget optimality**: The $186M budget represents a "sweet spot" where cost efficiency peaks; additional funding yields diminishing returns
2. **Solution robustness**: Selected corridors remain stable across ±30% demand variations, driven by structural network properties
3. **Critical path**: Corridor 21 (47.1 km) determines overall project duration and cannot be parallelized beyond 2-3 teams
4. **Winter productivity**: Reducing the winter penalty from -40% to -30% would save 1 year—more cost-effective than adding teams

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy geopandas shapely fiona matplotlib seaborn scikit-learn gurobipy
```

### Running the Analysis
1. Clone the repository
2. Navigate to `final_code/Final Code.ipynb`
3. Execute cells sequentially to reproduce:
   - Phase 1: Corridor discovery and clustering
   - Phase 2: ILP corridor selection
   - Phase 3: Construction scheduling optimization
   - Sensitivity analysis

## 📚 Data Sources

- **Candidate Segments**: Montreal GeoPackage (Q4 2024)
- **Existing REV Network**: Official municipal GeoJSON
- **Demand Data**: BIXI Montreal trip database (2024, 13M trips)
- **Road Network**: OpenStreetMap via Python OSMnx

## 👥 Team

- **Faye Wu** – Team Lead & Data Scientist
- Maral Vahedi
- Tia Qiu
- Helia Mahmood Zadeh
- Fares Joni

*McGill University – MGSC-662-076 Decision Analytics*
*Instructor: Professor Javad Nasiry*
*Fall 2025*

## 📄 License

This project is for academic purposes at McGill University.

---

**Keywords**: `geospatial analysis` `optimization` `integer linear programming` `mixed-integer programming` `Gurobi` `DBSCAN` `GIS` `urban mobility` `infrastructure planning` `bike network` `Montreal` `REV`

---

Let me know if you'd like me to adjust any sections or add more technical details!
