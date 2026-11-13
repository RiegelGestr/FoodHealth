# Food co-purchasing networks encode geographic disparities in cardiometabolic health

Antonio Desiderio (DTU; ISI Foundation; Centro Ricerche Enrico Fermi), Leonardo Rodovero (DTU), Sune Lehmann (DTU; SODAS, University of Copenhagen).

Corresponding authors: antde@dtu.dk, sljo@dtu.dk.

## Abstract

Unhealthy diets are a major driver of cardiometabolic disease, yet the geospatial structure of dietary behavior and its links to population health remain poorly understood.

While large-scale retail transaction data offer a unique view of population dietary behavior, conventional approaches reduce purchases to isolated items, not accounting for how foods are actually combined.

Here, we analyze 51 million grocery receipts across 95 Danish municipalities using a statistically validated bipartite network framework to isolate co-purchases that product popularity alone cannot explain.

We find that, although municipalities buy largely the same products, their co-purchasing networks reorganize along a continuous urban-to-peripheral gradient in how those products are combined.

The network backbone can be resolved into modular dietary communities whose local cohesion allows us to predict cardiometabolic prescriptions, explaining a quarter to a half of the variance left after sociodemographic adjustment, beyond what product prevalence alone accounts for.

Ultra-processed foods (UPFs) show no spatial gradient in prevalence and are located at the network periphery, where they share baskets with fresh foods but rarely form the combinations that hold the network together.

Taken together, our findings show that geographic dietary differences are encoded not only in what people purchase, but in how foods are systematically combined within shopping baskets, offering a scalable network approach for population nutritional epidemiology.

## Code

`figures.ipynb` redraws the paper figures from already-validated networks. It does not fit the bipartite configuration model. Backbones were obtained with a standard BiCM library (Saracco et al.).

Receipts are not in this repository. Health, population, and income are from Statistics Denmark (MEDI1, BY2, INDKF132). Polygons are GADM.

Point `paths.py` at a local `data/` folder.

- `municipal_edges/{kommune_id}.parquet` — `product_i`, `product_j`, `weight`
- `national_edges.parquet` — `product_i`, `product_j`, `z_score`
- `pair_stats.parquet` — `kommune_id`, `product_i`, `product_j`, `N_ij`, `N`, `n_i`, `n_j`
- `products.parquet` — `brand_micro_cat`, `nova`, `fscore`; optional `meta`, `level_2_meso`
- `partition.parquet` — `brand_micro_cat`, `community_id` (required; the notebook does not re-run Louvain for names)
- `health.csv` — `municipality`, `log_pop`, `share_under30`, `share_over60`, `affluence_index`, prescription rates
- `health_age.csv` — same rates with `age_group` equal to `60+`
- `kommuner.geojson` — `GID_2`, `NAME_1`, `NAME_2`
- `tie_carriage.parquet` — optional; `pair_class`, `gamma`

`kommune_id` is the polygon id. Bornholm is dropped.

## Run

From this folder:

```
jupyter notebook figures.ipynb
```

numpy, pandas, networkx, scipy, matplotlib, geopandas, scikit-learn, statsmodels, python-louvain, libpysal, esda.

Figures go to `figure/`.
