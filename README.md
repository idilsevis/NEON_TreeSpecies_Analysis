# NEON_TreeSpecies_Analysis
This repository contains a Colab notebook (`NEON_TreeSpecies_Analysis.ipynb`) and related outputs for analyzing tree species annotations from the [NEON](https://www.neonscience.org/) project and the [NeonTreeEvaluation dataset](https://github.com/weecology/NeonTreeEvaluation).

## Data Sources

- **NEON field data (`NEON_struct-plant`)**  
  Individual tree crown (ITC) CSV files with geographic coordinates and species labels. These data are part of NEON's *Structure-from-Motion Individual Tree Dataset*.  
  Example: `SJER_2019-11_individuals_with_coords.csv`

- **NeonTreeEvaluation dataset (`weecology-NeonTreeEvaluation-d0b90bc`)**  
  Contains crown annotations (XML/GPKG) with polygons, RGB/CHM/LiDAR/Hyperspectral imagery, and species-matching files.  
  Original repository: [weecology/NeonTreeEvaluation](https://github.com/weecology/NeonTreeEvaluation)

## What the Notebook Does

1. **Explore NEON ITC CSVs**  
   Lists and inspects tree-level CSVs, focusing on years 2017–2020.

2. **Extract Field Points**  
   Converts ITC CSVs into GeoDataFrames (`geopandas`) and reprojects them to EPSG:5070.

3. **Load Polygon Annotations**  
   Reads polygons from `voc_polygons_with_species_FIXED.gpkg` and extracts year/site info.

4. **Join Field ↔ Annotation Data**  
   - Coalesces species columns from multiple naming conventions  
   - Selects best match per polygon (using `match_type` + distance ranking)  
   - Assigns confidence levels (`high`, `medium`, `none`)  

5. **Reports & Summaries**  
   - Species counts per XML / RGB file  
   - Pivot tables for species × file  
   - Top 20 most common species  
   - Coverage statistics (annotations vs. matched species) per file and per site  

All results are saved into `annotations_with_species/reports/`.

## Outputs

- `Tree_to_FieldSpecies_JOINED_dedup.csv` – deduplicated matches  
- `Tree_to_FieldSpecies_JOINED_SAFE.csv` – only high/medium confidence matches  
- Reports (CSV pivot tables, top species, coverage per file/site)

## References
National Ecological Observatory Network (NEON): https://data.neonscience.org
NeonTreeEvaluation dataset: https://github.com/weecology/NeonTreeEvaluation

## Requirements

- Python 3.10+  
- [Google Colab](https://colab.research.google.com/) environment recommended  
- Main libraries: `pandas`, `geopandas`, `shapely`, `fiona`, `rtree`  

Install with:
```bash
pip install geopandas fiona shapely pyproj rtree
