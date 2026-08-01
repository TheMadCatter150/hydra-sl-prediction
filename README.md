# hydra-sl-prediction
Code accompanying "Genome-wide synthetic lethality prediction in breast cancer identifies VEGFA as a recurrent angiogenic vulnerability hub."
Submitted to PLOS ONE.

## Environment
- Python 3.x, PyTorch 2.2.1 (CUDA 11.8), PyTorch Geometric
- Developed and run on Google Colab, Tesla T4 GPU, 13GB RAM
- Install: `pip install -r requirements.txt`

## Data sources (not included in this repo: download separately)
- SynLethDB SL/non-SL pairs: synlethdb.comp.nus.edu.sg
- TCGA BRCA mutation data (data_mutations.txt): portal.gdc.cancer.gov
- METABRIC mutation data: cBioPortal (brca_metabric)
- KEGG c2.cp gene sets: gsea-msigdb.org (registration required)
- STRING PPI (v11, combined_score ≥ 400): string-db.org
- COSMIC Cancer Gene Census (included in the code of this repo)

Place downloaded files under a local `Files/` directory matching the
paths referenced near the top of the notebook (`DATA_DIR`, `PPI_FILE_PATH`,
`COSMIC_CGC_FILE`), or set the `HYDRA_DATA_DIR` / `HYDRA_PPI_FILE`
environment variables to point elsewhere.

## Running
Open `HYDRA_main.ipynb` in Colab or Jupyter and run cells in order.
Cell 1 installs dependencies; Cells 2–3 load data; Cells 4–5 train the
main PPI-only ensemble; Cell 6 runs the DDGCN baseline; Cell 7 runs the
three-condition ablation; Cell 8 scores all novel pairs; Cell 9 runs
METABRIC cross-cohort validation; Cells 10+ reproduce paper figures

## Known issues
- On first run in Colab, a numpy import error sometimes occurs after
  installing dependencies. If this happens, restart the runtime and
  re-run `pip install -r requirements.txt`: the reinstall will be fast
  since packages are already cached.

Note: full execution requires the raw data files listed above. These
files require free registration with their respective providers
and are not redistributed here due to licensing terms. The notebook
documents the exact transformations applied (see Cell 3 for renaming,
Cell 4 for feature construction) so results can be independently
verified against the described methodology even without the original
files.
