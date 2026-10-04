# Organic photovoltaic property prediction

This repository predicts four molecular properties from a SMILES string with a residual graph neural network:

| Key in the result | Property |
|---|---|
| `pce` | Power conversion efficiency from the Scharber model (%) |
| `voc` | Open-circuit voltage from the Scharber model (V) |
| `jsc` | Short-circuit current density from the Scharber model (mA/cm²) |
| `e_gap_alpha` | Bandgap (eV) |

PCE, Voc, and Jsc are Scharber-model values with a fixed fill factor of 0.65. They are not measurements from a fabricated solar cell. Each result is a single number, not a confidence interval.

## Website

Interactive demo, one SMILES string at a time:

https://gitlabnsclbio.jbnu.ac.kr/graphopvs/

The site has no public API, no batch-prediction endpoint, and no published rate quota. A SMILES string entered there is sent to the server only to compute that prediction. It is not added to the public dataset. To screen many molecules, or to keep structures on your own computer, use the notebook below.

The website also has two tools that are not in this notebook:

1. **Dataset analysis.** Filter and export the stored HCEP table. This does not run a new calculation.
2. **Similarity search.** Rank stored molecules by the Tanimoto coefficient on RDKit fingerprints (threshold 0.2 to 1.0). A high score means a similar structure, not a predicted device efficiency.

## Install

Use Python 3.9. Run these commands from the repository folder.

```bash
git clone https://github.com/AsadKhanJBNU/opvs.git
cd opvs
python3.9 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install torch==2.2.1 torch-geometric==2.5.0 rdkit==2023.9.5 pandas==2.1.4 jupyter matplotlib numpy
```

On Windows, activate the environment with `.venv\Scripts\activate`.

`environment.yml` is the Linux environment used for training, including `torch==2.2.1+cu118`. It is not required for prediction. Prediction in the notebook is set to CPU.

## Run a prediction

Saved weights are already in `saved_models/`:

- `pcemodel.model`
- `vocmodel.model`
- `jscmodel.model`
- `e_gap_alphamodel.model`

Start Jupyter from this same folder, so the imports `models` and `saved_models` resolve:

```bash
jupyter notebook PredicationFunction.ipynb
```

In the notebook, use **Run All**. The last code cell predicts one molecule:

```python
smileslist = ['C12=C(C=C3C(=C1)C=CC=C3)C=C4C(=C2)C=CC=C4']
predictions_result = makePredictions(smileslist)
print(predictions_result)
```

The printed value is a dictionary. Each key holds one number per input SMILES, in the same order as `smileslist`.

## Run a batch

Replace the list with as many valid SMILES strings as you need, then run that cell again. The notebook scores them in groups of 64.

```python
smileslist = [
    "CCO",
    "c1ccccc1",
    "C12=C(C=C3C(=C1)C=CC=C3)C=C4C(=C2)C=CC=C4",
]
predictions_result = makePredictions(smileslist)
print(predictions_result)
```

Use RDKit-readable SMILES. An invalid string stops the run. Do not shuffle the loader: `PredicationFunction.ipynb` sets `shuffle=False` so result position `i` belongs to SMILES `i`.

## What the code does

`makePredictions` calls the four saved models one after another. Each model is the residual gated graph network in `models/Predictor_resgatedgraphconvN.py`. RDKit and PyTorch Geometric turn each SMILES string into a molecular graph. The model returns one scalar per molecule.

## Contact

Basir Akbar (basirakbar98@gmail.com)

Asad Khan (asadkhan@jbnu.ac.kr)
