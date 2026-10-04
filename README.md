# Webserver
https://gitlabnsclbio.jbnu.ac.kr/graphopvs/

The site is an interactive research demo. It accepts one SMILES string at a time. It has no public API, no batch-prediction endpoint, and no published rate quota.

A SMILES string entered on the website is sent to the server only to compute that prediction. It is not added to the public HCEP table. Structures that should not leave your computer should be run locally.

## Batch prediction

Batch prediction is local, not on the website. Open `PredicationFunction.ipynb` and call `makePredictions` with a list of SMILES. The notebook loads the saved PCE, Voc, Jsc, and bandgap models and runs them on CPU in batches of 64. Results are returned in the same order as the input list.

```python
smileslist = [
    "CCO",
    "c1ccccc1",
]
print(makePredictions(smileslist))
```

Local prediction uses PyTorch and a CPU, as set in the notebook. The Python environment is `environment.yml`. A GPU is optional.

## What the three tools do

1. **Dataset analysis.** Filters and displays the stored HCEP table (PCE, Voc, Jsc, bandgap) and can export the filtered rows. It does not run a new calculation.
2. **Property prediction.** Runs the trained residual graph network on one SMILES string and returns PCE, Voc, Jsc, and bandgap. A separate model returns an OMDB bandgap. PCE, Voc, and Jsc are Scharber-model values with a fixed fill factor of 0.65. They are not fabricated-device measurements. The model returns a single number, not a confidence interval.
3. **Similarity search.** Ranks molecules in the stored table by the Tanimoto coefficient on RDKit fingerprints. The threshold can be set from 0.2 to 1.0. A high score means a similar structure. It is not a prediction of device efficiency.

## Developer Contact
Basir Akbar (Contact basirakbar98@gmail.com)
Asad Khan (Contact asadkhan@jbnu.ac.kr)

