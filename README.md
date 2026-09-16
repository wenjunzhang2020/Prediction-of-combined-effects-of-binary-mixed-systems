README.md
Prediction of combined effects of binary mixed systems of typical environmental pollutants
This repository contains the dataset, code, trained model weights, and preprocessing pipelines for our multimodal attention fusion (CIAF-WGANGP) model, which classifies joint toxicity interaction types of binary chemical mixtures across five toxicity endpoints: reproductive toxicity, neurotoxicity, immunotoxicity, hepatotoxicity, and developmental toxicity.
GitHub repo: https://github.com/wenjunzhang2020/Prediction-of-combined-effects-of-binary-mixed-systems.git
Note: Due to GitHub file‑size constraints, large‑size files including `QSAR train data`, `original data(reference info)`, and five `_modelAD2.pth` applicability‑domain parameter files are not stored in GitHub. These files are archived at Zenodo:
[https://doi.org/10.5281/zenodo.21271714](https://doi.org/10.5281/zenodo.21271714)
Please download these files and place them into the corresponding local folders before executing notebooks.

## Repository Overview
Notebooks (Core Workflow)
Filename	Description
Applicability Domain and AD Prediction of binary mixed system of typical environmental pollutants.ipynb	Applicability Domain (AD) calculation and prediction for binary mixtures. The trained AD parameter files for five toxicity endpoints are named with suffix _modelAD.pth.
CIAF-WGANGP Model & SHAP & Global modal self-attention weight .ipynb	Main model training pipeline, SHAP interpretation, and global multimodal self-attention weight analysis.
Correlation analysis of molecular toxicology mechanism.ipynb	Molecular descriptor–toxicity association and statistical analysis.
DNN-QSAR for Activity probability in assay.ipynb	QSAR-DNN submodel to predict ToxCast in vitro assay responses for compounds lacking experimental ToxCast measurements.
Prediction of combined effects of binary mixed systems of typical environmental pollutants at five kinds of toxicity endpoints.ipynb	Inference script to predict mixture joint interaction types for new binary chemical combinations across all five toxicity endpoints.


## Model weight & scaler files
1.	QSAR-DNN submodel (ToxCast assay prediction)
•	*_hybrid_dnn_best.pth: Trained weights of QSAR-DNN models
•	*_hybrid_scaler.pkl: Feature scaling parameters for QSAR-DNN inputs
2.	Applicability Domain models
•	*_modelAD.pth: AD model weights for reproductive / neuro / immuno / hepato / developmental toxicity endpoints

## Datasets
1.	*-traindata-Enumerator.xlsx: Machine-readable training datasets for each toxicity endpoint, after SMILES enumeration augmentation.
2.	Folder original data from literature: Raw manually extracted mixture toxicity data retrieved from published peer-reviewed toxicology studies.
3.	Folder QSAR train data: Training data for the ToxCast QSAR-DNN submodels, downloaded from EPA CompTox ToxCast database (https://www.epa.gov/comptox-tools/exploring-toxcast-data).
4.	chemical-to-predict.xlsx: Example input file containing candidate chemicals for mixture prediction.
Note: Large raw dataset folders (`QSAR train data`, `original data(reference info)`) are hosted on Zenodo. Download and unpack into your local working directory.

## Environment setup
Python >=3.9
PyTorch >=1.10
numpy
pandas
rdkit
shap
scikit-learn
matplotlib
seaborn
All Jupyter notebooks are developed and tested under jupyter-clean environment.

## Reproduction workflow
1.	Prepare raw data: Raw literature data is stored in original data from literature. The curated training sets (*-traindata-Enumerator.xlsx) are ready for model training.
2.	Train QSAR-DNN submodels: Run DNN-QSAR for Activity probability in assay.ipynb to predict ToxCast assay responses for compounds without experimental ToxCast measurements. Outputs: *_hybrid_dnn_best.pth and *_hybrid_scaler.pkl.
3.	Train main CIAF-WGANGP model & interpretability analysis: Run CIAF-WGANGP Model & SHAP & Global modal self-attention weight .ipynb to train the multimodal classification model, compute SHAP values and attention weights.
4.	Applicability Domain evaluation: Run Applicability Domain and AD Prediction ...ipynb to compute Mahalanobis distance, 5-NN distance and Tanimoto similarity to judge whether a new mixture falls within the model applicability domain.
5.	Predict new binary mixtures: Run Prediction of combined effects of binary mixed systems ...ipynb using chemical-to-predict.xlsx as input, to obtain predicted joint toxicity interaction classes.
6.	Molecular toxicology correlation analysis: Run Correlation analysis of molecular toxicology mechanism.ipynb.
  
## Important Notes & Limitations
1.	The model predicts five mixture interaction classes: synergistic, antagonistic, additive, independent, unreported.
2.	Predictions are hypothetical 28-day exposure scenario, designed for relative hazard screening and ranking, not equivalent to real-world long-term in vivo toxicity results.
3.	Human-relevant predictions rely on human in vitro ToxCast assay features, not human in vivo or epidemiological data.
4.	Reported model performance metrics are single-point estimates from a fixed stratified train/test split. Uncertainty/variability of performance metrics is not quantified in this work.
5.	For persistent pollutants such as PFAS and heavy metals, 28-day simulation results cannot fully reflect cumulative long-term toxic outcomes and should be interpreted cautiously.

