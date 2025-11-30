# STEM LEAN FROM UAV LIDAR
### Measuring Tree Stem Lean Angle and Azimuth from Point Clouds

This repository contains a Jupyter/Colab notebook and an example dataset to compute **tree stem lean angle and azimuth** from UAV–LiDAR point clouds.  
The analysis is done in **Python on Google Colab**, so no local installation is required.

Main notebook: `STEM_LEAN_LIDAR.ipynb`.

---

## 🎯 Purpose

This repository is intended to:

- Provide a complete workflow for computing **stem lean** from LiDAR point clouds.
- Demonstrate how tree stem inclination can be used as a **biosensor of ground deformation** and as an indicator of landslide reactivation zones.
- Serve as a tutorial for studies on **landslides, slope stability, and vegetation deformation**.

---

## 📂 Repository Structure

Suggested folder structure:

```text
.
├── STEM_LEAN_LIDAR.ipynb          # main notebook (Google Colab)
├── data/
│   └── Exemple_tree.csv # example point cloud data (CSV format)
└── README.md                      # main description (may be in Indonesian)
└── README_EN.md                   # this English description
```

You can keep `README.md` in Indonesian and use `README_EN.md` as the English version.

---

## 🌲 Input Data: Point Cloud CSV

The notebook uses point cloud data in **CSV** format with the following columns:

- `X`  : X coordinate (e.g. UTM / local coordinates)
- `Y`  : Y coordinate
- `Z`  : elevation of the point (above sea level or another vertical datum)
- `tree_id` : tree identifier, used to separate points belonging to different trees
- `HeightAboveGround` : point height above the ground surface (height above ground)

Example rows:

| X         | Y          | Z       | tree_id | HeightAboveGround |
|----------:|-----------:|--------:|--------:|------------------:|
| 456782.12 | 9123450.55 | 103.55  | 1       | 5.23              |
| 456782.35 | 9123450.60 | 104.10  | 1       | 5.78              |
| 456783.00 | 9123451.10 | 110.20  | 2       | 10.45             |

Recommended example file name:

```text
data/Exemple_tree.csv
```

With the `tree_id` column, the notebook can process **each tree separately** (per-tree processing), estimate the stem axis, and compute lean angle and azimuth for every tree.

---

## 🌲 Concept: Stem Lean

The notebook focuses on two key metrics:

- **Lean angle (°)**  
  The inclination angle of the tree stem relative to the vertical axis  
  (0° = perfectly vertical, larger values = more tilted).

- **Lean azimuth (°)**  
  The direction of the stem tilt in the horizontal plane (0–360°).  
  By convention:
  - 0°   → North  
  - 90°  → East  
  - 180° → South  
  - 270° → West  

The spatial pattern of lean angle and azimuth can be used to:

- Identify **landslide reactivation zones**  
- Infer **mass-movement direction**  
- Link vegetation indicators with **subsurface structure** (e.g. from ERT)

---

## ⚙️ Dependencies & Environment

The notebook is designed to run on **Google Colab**.

Typical Python libraries (may vary depending on the final notebook):

- `numpy`
- `pandas`
- `matplotlib`
- `mpl_toolkits.mplot3d`
- (optional) `scipy` for PCA / stem axis fitting
- (optional) other geospatial libraries (`geopandas`, etc.)

In Colab, you can install additional packages, for example:

```python
!pip install numpy pandas matplotlib
```

(or adjust according to the actual notebook requirements).

---

## ▶️ How to Run the Notebook in Google Colab

1. **Open Colab and upload the notebook**

   - Go to: https://colab.research.google.com  
   - Click **Upload** and select `STEM_LEAN_LIDAR.ipynb`.

2. **Upload the point cloud CSV**

   - Open the **Files** panel (folder icon on the left).
   - Create a `data` folder (for cleanliness).
   - Upload the CSV file (e.g. `Exemple_tree.csv`) into that folder.
   - Adjust the path in the notebook, for example:
     ```python
     data_path = "/content/data/sample_tree_pointcloud.csv"
     ```

3. **Run the notebook cells**

   Typical sequence:
   - Import libraries
   - Load the CSV data
   - Group points by `tree_id`
   - Estimate stem axis for each tree
   - Compute lean angle and azimuth
   - Produce 2D/3D visualisations and summary plots

---

## 📈 Outputs

The notebook can produce:

- Tables / DataFrames containing:
  - `tree_id`
  - lean angle (°)
  - lean azimuth (°)
  - stem axis coordinates / vectors

- Visualisations:
  - 3D plots of point clouds and fitted stem axes
  - Histograms of lean angles
  - Scatter plots or directional diagrams of lean azimuths

These outputs can be used for:

- Vegetation deformation analysis
- Identifying critical slope zones
- Integration with other geospatial datasets (DEM, ERT, geomorphological maps, etc.)

---

## 🧩 Possible Extensions

The notebook can be extended to:

- Relate stem-lean patterns to:
  - Ground cracks
  - Flow accumulation channels
  - Low-resistivity zones from ERT
- Build:
  - Slope-scale stem-lean maps
  - Statistics per geomorphic zone (head, body, toe of landslide)
  - Combined morphology–vegetation–subsurface indicators

---

## 📜 License

You may use this script and repository structure for:

- Research
- Theses / dissertations
- Education and training

Please provide appropriate credit or citation if this method or script is used in scientific publications.

---
