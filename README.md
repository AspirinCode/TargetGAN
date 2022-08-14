# TargetGAN
It is the code for Deep Generative Model for Drug Design from Protein Target Sequence.
DeepTarget

Dependencies

The encoder and decoder for the SMILES uses the heteroencoder available as a package from [4]. The heteroencoder further requires this package to run properly on the ChEMBL or MOSES model. 
The encoder for the Protein sequence uses the pre-train model from [1].

Installation
1. Clone this repo.
2. Create conda environment from .yml file conda env create --file env.yml
3. Download dependencies Deep Drug Coder and molvecgen
4. move Deep-Drug-Coder/ddc_pub/ and molvecgen/molvecgen.

mv Deep-Drug-Coder/ddc_pub/ .
mv molvecgen/molvecgen tmp/
mv tmp/ molvecgen/

How to train the model.
1. Prepare the SMILES and Protein sequence. 
2. Encode the protein in advance using [1].
3. One can use the runfile (run.py) for a single script that does the entire process from encoding smiles to create a training set, create and train a model, followed by sampling and decoding latent vectors back into SMILES using default hyperparameters. 
Arguments:
-sf <Input SMILES file name>
-st <Output storage directory path [DEFAULT:"storage/example/"]>
-lf <Output latent file name [DEFAULT:"encoded_smiles.latent"], this will be put in the storage directory>
-ds <Output decoded SMILES file name [DEFAULT:"decoded_smiles.csv"], this will be put in the storage directory>
--n-epochs <Number of epochs to train the model for [DEFAULT: 2000]>
--sample-n <Give how many latent vectors for the model to sample after the last epoch has finished training. Default: 30000>
--encoder <The data set the pre-trained heteroencoder has been trained on [chembl|moses] [DEFAULT:chembl]> IMPORTANT: The ChEMBL-trained heteroencoder is NOT intended for use with the MOSES SMILES, just as the moses-trained model is not intended for use with the ChEMBL based SMILES files.
4. Once the training is complete you can sample it via the test function in the (run.py).

How to eval the results.
The evaluation is divided into three parts.
1. The basic properties of the generating molecule, which can be obtained by [3]
2. the protein target affinity calculation, which can be calculated by any open source for DTA or DAI model.
3. Evaluation of the binding capacity of the protein target, which requires the installation of  molecular docking software as well as the preparation of the pdb file.


Links
[1] Evaluating Protein Transfer Learning with TAPE

[2] ChEMBL

[3] Molecular Sets (MOSES): A benchmarking platform for molecular generation models

[4] Deep-Drug-Coder
