# mortalitree_testing

Coding experiments to support the [mortalitree](https://github.com/StanfordGeospatialCenter) project. Workflows for generating XYZ tile service URLs from Google Earth Engine, downloading tile imagery, and creating tile boundary grids for analysis.

## Repository Structure

```
mortalitree_testing/
├── data/              # Input AOI files and tile service lookups
├── images/            # (placeholder for screenshots/figures)
├── notebooks/         # Jupyter notebooks — the main workflows
├── output/            # Generated outputs (GeoJSON grids, URL lists)
└── tilesets/          # Downloaded tile imagery (z/x/y folder structure)
```

## Notebooks

| Notebook | Description |
|----------|-------------|
| [Step_01_get_tile_urls.ipynb](notebooks/Step_01_get_tile_urls.ipynb) | Uses **Google Earth Engine** to mosaic NAIP imagery for each available year over an AOI, then generates XYZ tile service URLs (RGB and IR) and exports them to CSV. (5 sections) |
| [Step_02_get_tiles.ipynb](notebooks/Step_02_get_tiles.ipynb) | Reads a CSV of tile service URLs and a GeoJSON AOI, computes the set of XYZ tiles at a given zoom level, then **downloads tile images in parallel** with retry logic, saving them as `.jpg` in a `z/x/y` folder structure. (12 sections) |
| [Step_03_tile_grid_generator.ipynb](notebooks/Step_03_tile_grid_generator.ipynb) | Generates a grid of **Web Mercator tile boundary polygons** at a specified zoom level that intersect an AOI. Exports tile metadata (ZXY values, centroids, corners) as GeoJSON or CSV (WKT). Includes an interactive [leafmap](https://leafmap.org/) preview of random tiles. (9 sections) |

## Data

| File | Description |
|------|-------------|
| [CZU_Fire_Perimeter_\*.geojson](data/CZU_Fire_Perimeter_-2212360052269988636.geojson) | CZU Lightning Complex fire perimeter boundary. |
| [DINS_2025_TCU\*.geojson](data/DINS_2025_TCU_September_Lightning_Complex_Public_View.geojson) | TCU September Lightning Complex damage inspection data. |
| [mortalitree_czu_download_bbox.geojson](data/mortalitree_czu_download_bbox.geojson) | Bounding box AOI for the CZU fire area tile downloads. |
| [stanford_campus.geojson](data/stanford_campus.geojson) | Stanford campus boundary (sample AOI). |
| [SantaClara_TattooParlors_2134.geojson](data/SantaClara_TattooParlors_2134.geojson) | Santa Clara County tattoo parlor locations (point-feature sample AOI). |
| [tile_services.csv](data/tile_services.csv) | Lookup table of named XYZ tile services (OSM, Stamen, GEE NAIP). |
| [gee_tiles.csv](data/gee_tiles.csv) | 20 Google Earth Engine NAIP tile service URLs (RGB + IR, 2003–2022). |

## Output

| File | Description |
|------|-------------|
| [tile_urls.csv](output/tile_urls.csv) | Generated GEE NAIP tile service URLs (RGB + IR, 2003–2022) for use by downstream notebooks. |
| [Z17_CZU_tile_boundary_grid.geojson](output/Z17_CZU_tile_boundary_grid.geojson) | Zoom-17 tile boundary grid clipped to the CZU fire perimeter. |

## Key Libraries

- [mercantile](https://github.com/mapbox/mercantile) — Spherical Mercator tile calculations
- [geopandas](https://geopandas.org/) — Geographic data manipulation
- [shapely](https://shapely.readthedocs.io/) — Geometric operations
- [leafmap](https://leafmap.org/) — Interactive geospatial visualization
- [Google Earth Engine Python API](https://developers.google.com/earth-engine/guides/python_install) — Access to NAIP and other satellite imagery

## License

See [LICENSE](LICENSE) for details.
