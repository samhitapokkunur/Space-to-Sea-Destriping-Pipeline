# Muench Destriping Experiment Files

Drop these files into the root of your Git repo, next to your existing pipeline file.

## Files

- `sweep.py`  
  Runs many randomized Latin Hypercube parameter experiments.

- `run_experiment.py`  
  Runs one exact parameter setting.

- `experiment_utils.py`  
  Helper functions used by both scripts.

## Important

Your existing pipeline file must contain:

```python
process_rgba(...)
```

For example, if your existing file is:

```text
modified_muench.py
```

then run with:

```bash
--pipeline-module modified_muench
```

Do not include `.py`.

## Install dependencies

From the repo root:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

If the repo does not have `requirements.txt`, install the common ones:

```bash
pip install numpy scipy pywavelets rasterio affine scikit-image matplotlib opencv-python
```

## Run many randomized outputs

```bash
python sweep.py \
  --input test_data/chlor_a_oceancolor.tif \
  --out-root experiments/muench_random \
  --runs 50 \
  --pipeline-module modified_muench \
  --enhance-contrast
```

## Run fewer outputs first

Start with 5 to make sure everything works:

```bash
python sweep.py \
  --input test_data/chlor_a_oceancolor.tif \
  --out-root experiments/test_5_runs \
  --runs 5 \
  --pipeline-module modified_muench \
  --enhance-contrast
```

## Run one exact output

```bash
python run_experiment.py \
  --input test_data/chlor_a_oceancolor.tif \
  --out-dir experiments/manual_dv6_sv2p4 \
  --pipeline-module modified_muench \
  --dec-v 6 \
  --sigma-v 2.4 \
  --dec-h 0 \
  --sigma-h 0 \
  --enhance-contrast
```

## Output structure

The sweep will create folders like:

```text
experiments/muench_random/
├── parameter_runs_YYYYMMDD_HHMMSS.csv
├── run_000_dv06_sv2p40_dh00_sh0p00_db25/
│   ├── params.json
│   ├── yourimage_run_000_..._processed.tif
│   └── intermediates/
├── run_001_dv11_sv9p32_dh02_sh3p21_sym10/
│   ├── params.json
│   ├── yourimage_run_001_..._processed.tif
│   └── intermediates/
```

Each run folder saves:

- the processed GeoTIFF
- intermediate outputs
- `params.json`
- one master CSV with all parameter values

## Note about wavelet

Your current pipeline likely calls:

```python
muench_complete_modified(..., wavelet="db25")
```

inside `process_rgba`.

That means `sweep.py` records a randomized wavelet name in the folder/CSV, but the actual algorithm may still use `db25`.

To truly randomize wavelet too, update `process_rgba()` to accept a `wavelet` argument and pass it into `muench_complete_modified()`.
