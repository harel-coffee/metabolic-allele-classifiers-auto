[![MIT](https://img.shields.io/pypi/l/Escher.svg)](https://github.com/erolkavvas/escher/blob/master/LICENSE)

# Metabolic Network Classifiers

Metabolic Network Classifiers (MNCs) are flux balance analysis-based genome classifiers that achieve prediction accuracy on par with state-of-the-art machine learning approaches while enabling a mechanistic interpretation of the genotype-phenotype map. MNCs thus provide a FBA framework for microbial genome-wide association studies (GWAS) (preprint SOON). Inference and computation of MNCs utilize cobrascape (https://github.com/erolkavvas/cobrascape), which wraps around COBRApy package (https://github.com/opencobra/cobrapy) to model a population of strain-specific genome-scale models (GEMs) at allelic resolution.

![cobrafig](/MNC\_overview.png?raw=true)

### Generating Metabolic Network Classifiers
Run both `gen_mnc_samples.py` and `eval_mnc_samples.py`
1. Run `$ python gen_mnc_samples.py -f INPUT_DIR -s NUM_SAMPLES -o MNC_DIR [optional parameters...]`
	- Generates a MNC samples. Requires performing flux variability analysis (popFVA) which is very computationally expensive. Recommend >1000 samples
2. Run `$ python eval_mnc_samples.py -f MNC_DIR [--testset --bicthresh]`
	- Optimize the MNC for the training set or testset.

An ensemble of sampled MNCs can be generated by running steps 2 and 3 multiple times for the same output directory. The input parameters must be consistent for the same output directory. This is helpful because generating samples takes a long time so the simulations are likely to be interrupted at some point.

### Analyzing Metabolic Network Classifiers
Once a large number of MNCs has been generated (~1000+), they can be analyzed to study the genetic and metabolic basis for the GWAS dataset.
1. See `analyze_mncs.ipynb`

### Input Data
- The following files are to be placed in INPUT_DIR. The files should be named exactly as described below.
    - `genome-scale model`          (filename: 'MODEL_FILE.json')       REQUIRED  
    - `strain allele matrix`        (filename: 'X_ALLELES_FILE.csv')    REQUIRED  
    - `strain phenotypes matrix`    (filename: 'Y_PHENOTYPES_FILE.csv') REQUIRED  
    - GENE_LIST_FILE              	(filename: 'GENE_LIST_FILE.csv')    OPTIONAL - highly recommended <200 genes. otherwise sample deeply  
- JSON object describing mapping of genes to pathways for the organism (see `cobra_model/gene_to_pathways_filt.json` for example)
- JSON object describing mapping of gene ids to names (see `cobra_model/gene_to_name.json` for example)

Installation
	git clone https://github.com/erolkavvas/metabolic-network-classifiers.git

Strain allele matrix and strain phenotypes matrix from (https://rdcu.be/9rHj) and cobra model from (https://rdcu.be/bG6JO).
