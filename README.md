# Large-Scale Hybrid Residual Graph Neural Networks with Transfer Learning for Multi-Property Prediction in Organic Photovoltaics and Organic Materials: From Computational Screening to Experimental Validation
Rational design of high-performance Organic Photovoltaics (OPVs) requires understanding structure-property relationships governing open-circuit voltage, short-circuit current density, and bandgap, with power conversion efficiency being the most crucial property for overall device performance. This study develops an experimentally validated Hybrid Residual Graph Neural Network (RGNN) model for predicting key OPVs properties. The Harvard Clean Energy Project (HCEP) dataset contains over 2.3 million molecular datapoints with Simplified Molecular Input Line Entry System (SMILES) representations. After preprocessing to remove null values, duplicates, and invalid SMILES using RDKit, the dataset is divided into training, testing, and validation sets. Hyperparameter optimization is performed using the Optuna framework, achieving R² values exceeding 0.90 with low MAE and RMSE across all target properties. Further, similarity analysis is performed using the Tanimoto index with reference molecules for each property. Transfer learning is implemented by fine-tuning the pre-trained RGNN on the OMDB dataset (12,500 organic molecules), achieving superior performance compared to state-of-the-art methods for bandgap prediction of organic materials. Experimental validation using independent literature data demonstrates strong alignment between predicted and experimental outcomes. Finally, we develop a user-friendly web server providing dataset analysis, property prediction, and similarity analysis functionalities, addressing critical needs in computational materials science through a single accessible interface.

<img width="12210" height="6310" alt="graphicalAbstractHarvard" src="https://github.com/user-attachments/assets/f197d39a-1f01-4019-8b1f-f0e444deb2b1" />

# Webserver
https://gitlabnsclbio.jbnu.ac.kr/graphopvs/
## Developer Contact
Basir Akbar (Contact basirakbar98@gmail.com)
Asad Khan (Contact asadkhan@jbnu.ac.kr)

