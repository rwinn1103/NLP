# What does it take to bake a cake? The RecipeRef corpus and anaphora resolution in procedural text

## Introduction 

This repository contains code and experiment results introduced in the following paper:

- [What does it take to bake a cake? The RecipeRef corpus and anaphora resolution in procedural text](https://aclanthology.org/2022.findings-acl.275/)

- Biaoyan Fang, Timothy Baldwin and Karin Verspoor

- In Finding of ACL 2022

- [LINK TO ORIGINAL REPOSITORY](https://github.com/biaoyanf/RecipeRef)

## Dataset

- For the data and detailed annotation guideline of the RecipeRef corpus, please refer to [RecipeRef dataset](https://data.mendeley.com/datasets/rcyskfvdv7/1)

## Getting Started (MUST BE ON A LINUX OPERATING SYSTEM)
- Create a python version 3.6 environemnt
- run `pip install tensorflow==1.12.0`
- run `pip install scikit-learn==0.22.2`
- Install python (preference 3) requirement: `pip install -r requirements.txt`
- Download [GloVe](https://nlp.stanford.edu/projects/glove/) embeddings and also another version [glove_50_300_2.txt](https://drive.google.com/file/d/1fkifqZzdzsOEo0DXMzCFjiNXqsKG_cHi). Place both of these within the main respository folder.
- Download [RecipeRef dataset](https://data.mendeley.com/datasets/rcyskfvdv7/1). Utilize either the entire dataset or the 80 recipe version. The data must be formatted to all be included in a `data` directory in this repository. Moreover, it must be partitioned into separate test/dev/train folders within said `data` directory. Lastly, make sure to create a `full` folder than contains ALL annotations inside the `data` directory. It should be noted that the `data` directory should only contain one type of data (i.e., considering state changes OR not considering state changes). Example path would be the following: './NLP/data/full/'
- run `bash setup_all.sh`
- Install [brat evalation tool](https://bitbucket.org/nicta_biomed/brateval/downloads/) - ENSURE TO DOWNLOAD ENTIRE REPOSITORY ZIP AND FOLLOW INCLUDED README. All brateval scripts should be held in the main repository directory (i.e., ./NLP/)
- We use nltk to tokenzize the brat file for training and generating the jsonlines files. Our code can be found in [convert_brat_into_training_format-clear.ipynb](https://github.com/biaoyanf/RecipeRef/blob/main/convert_brat_into_training_format-clear.ipynb)
-To run notebook via command line, do the following:
  `pip install ipython`
  `sudo install --upgrade nbconvert`
  `sudo apt install jupyter-core`
- Also, should be noted that original provided notebook file in the original GitHub respository was missing required dependencies. Had to add the following at the top:
  `import nltk`
  `nltk.download('punkt')`
- Utilize the notebook file to acquire `dev.english.jsonlines`, `train.english.jslonlines`, and `test.english.jslonlines`. All of these can be acquired by changing the chosen output at the bottom of the notebook file. Also be sure to change the harded paths to fit your relevant machine (e.g., remove 'robert' in the path).
- Place all JSONLINES files into the data directory that you created previously
- Need to download ELMO data from [here](https://tfhub.dev/google/elmo/3) and place all files within this main directory. Change hard coded paths in `cach_elmo.py` and `anaphora_model.py` to your relevant machine.

- FOR A COMPLETE TIMELINE OF ALL ISSUES RAN INTO AND THEIR RELEVANT SOLUTIONS OF THE ORIGINAL REPOSITORY CLICK [HERE](https://docs.google.com/document/d/1jzPgeGH5G2O5fWHEdDr2PBEdsJW0TXDoR6a8NdV92Jw/edit?usp=sharing)

## Training Instructions
- Experiment configurations are found in `experiments.conf`
- Choose an experiment that you would like to run, e.g. `bridging`
- First run the command `Bash setup_training.sh` - THIS ONLY NEEDS TO BE DONE ONCE PER DATASET
- Training: `python train_folds.py <experiment>`
- Checkpoints are stored in the `logs` directory
- Prediction results are stored in the `prediction` directory


## Evaluation
- Evaluation: `python evaluate_folds.py <experiment>`
- Evaluation tool provides differnet settings, `exact` and `relax` mention matching. For this paper, we use `exact` mention matching

An example sequence to run an experiment and receieve results:

  `bash setup_all.sh`
  
  `bash setup_training.sh`
  
  `python train_folds.py joint_train`
  
  `python evaluate_folds.py joint_train`
