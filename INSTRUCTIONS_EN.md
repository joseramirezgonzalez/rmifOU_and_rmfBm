# Albatross project: upload and reconstruction instructions

## 1. Files and destinations

This delivery contains six ZIP files, each smaller than 25 MB.

- **GitHub:** upload all five `ALBATROS_GITHUB_PARTE_XX_DE_05.zip` files.
- **Overleaf:** import `ALBATROS_OVERLEAF.zip` as a separate project.
- Upload this **INSTRUCTIONS_EN.md** file alongside the five GitHub archives.
- Do not combine the files into another large ZIP.

The five GitHub archives contain different files from one analysis project. All five are required. They contain code, data and numerical results, with no image files, PDFs or manuscripts.

## 2. Reconstruct the analysis repository

Download all five GitHub ZIP files. Extract their contents into **one shared destination folder**, preserving paths and merging subfolders with matching names. Do not replace an entire folder with a later part and do not keep one separate project directory per ZIP.

On macOS or Linux, open a terminal in the folder containing the five archives and run:

```sh
mkdir -p ALBATROS_REPOSITORY
for part in ALBATROS_GITHUB_PARTE_*_DE_05.zip; do
    unzip -q "$part" -d ALBATROS_REPOSITORY
done
```

The reconstructed project must have `README.md`, `codes/`, `datos/`, `resultados_ajustes/`, `results/` and `predictivos/` under the same root.

## 3. Repository structure

| Directory | Contents |
|---|---|
| `codes/` | Documented R and Python code for cleaning, episode/bridge extraction, original and boundary inference, selection, simulation, comparison and figure generation. |
| `datos/` | Supplied data, retained GPS observations, complete series, nest-residence and short/long-trip episodes, and the 16 spatial bridge inputs. See `datos/LEER_DATOS.md`. |
| `resultados_ajustes/01_originales/` | All 256 original fits, diagnostics and saved optimization stages. |
| `resultados_ajustes/02_fronteras/` | The boundary plan, all 50 completed fits and diagnostics. |
| `results/` | AIC rankings, parameter summaries, numerical tables and audits. |
| `predictivos/` | Saved simulated trajectories, occupancy fields, spatial geometries and comparisons, organized by bird and trip. |
| `analisis_temporal/` | Temporal-analysis code, inputs, fitted results and validation outputs. |
| `figures_spatial/` | Numerical comparison results required by historical scripts. Despite its name, this folder contains no image files in the GitHub package. |
| `research/`, `theory/` | Available provenance notes and verification reports, with LaTeX manuscripts excluded. |

CSV files contain tables. RDS files contain R objects, including fitted models, trajectories and occupancy fields. GeoPackage (`.gpkg`) files contain numerical spatial geometries; they are not rendered images.

Some comparison files remain in both historical locations expected by existing scripts. These are copies, not additional experiments. Original script comments and historical documentation have been preserved; this English guide explains the distribution and its use.

## 4. Check saved results without fitting or simulating

Open R with `ALBATROS_REPOSITORY` as its working directory:

```r
source("codes/00_USAR_PAQUETE.R", encoding = "UTF-8")
estado_paquete()
```

This command only reads saved data and results. The supplied project was verified to contain 8,278 retained GPS observations, nine birds, 16 long trips, 84 short trips, 256 original fits and 50 completed boundary fits.

Dependencies are documented within the scripts. Historical configurations may retain the original computer's absolute paths; use the portable entry point above or explicitly configure paths before starting a new analysis.

## 5. Regenerate figures from saved results

Figure-generation code is included; rendered images are excluded from GitHub. Run from the reconstructed project root:

```sh
Rscript codes/figuras_presentacion/01_MAPAS_INDIVIDUALES.R . imagenes_regeneradas/individuales
Rscript codes/figuras_presentacion/02_COMPARACIONES_Y_SIMULACIONES.R . imagenes_regeneradas/comparaciones
Rscript codes/figuras_presentacion/03_DISTRIBUCIONES_DURACION.R . imagenes_regeneradas/temporales
```

These presentation scripts use saved fits, simulations and fields; they do not refit models or simulate new paths. By contrast, `generar_mapas_ganadores()` generates new simulations and is unnecessary for inspecting existing results.

The supplied `.gitignore` excludes rendered images, PDFs, LaTeX files and build/cache files from ordinary Git tracking.

## 6. Compile in Overleaf

1. Import `ALBATROS_OVERLEAF.zip` as a new project.
2. Select **pdfLaTeX** as the compiler.
3. Select **main_N.tex** as the main document to compile the article.
4. Select **supplementary_N.tex** as the main document to compile the supplement.
5. Preserve `figures/`, `figures_clean/` and `figures_spatial/` in their supplied locations.

Both TeX files include all text, tables and bibliography. They do not require BibTeX, R, Python or the GitHub analysis files to compile. All 35 referenced figures are included at their original quality. Both documents compiled successfully with these dependencies using pdfLaTeX/latexmk. Overleaf generates the compiled PDFs; redundant compiled copies are not included.

## 7. Source and integrity

Source supplied by the author: `ALBATROS_MANUSCRITO_SUPLEMENTO 2.zip`. The selected manuscripts are `main_N.tex` and `supplementary_N.tex`, rather than the older versions. Only relative figure paths were adjusted for the Overleaf root layout; scientific content was not changed.

No fits, simulations or model-selection procedures were rerun during packaging. `ARCHIVOS_ORIGINALES_SHA256.csv` records the sizes and SHA-256 hashes of the original analysis files retained in the repository. The English guides and `.gitignore` are distribution files, not original scientific inputs. Every retained original analysis file and every archive part was verified.
