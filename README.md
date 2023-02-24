# TFBMiner
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)

A data acquisition and analysis pipeline for the rapid identification of putative transcription factor-based biosensors.
## Synopsis
TFBMiner predicts putative transcription factor-based biosensors (TFBs) for a compound of interest firstly by identifying enzymes that sequentially metabolize the compound and linking them to form chains. Each chain is then processed to identify whether the enzymes are encoded by any metabolic  operons within bacterial genomes, and putative transcriptional regulators of the operons are predicted and scored based upon a conceptual model of how TFBs are frequently genetically organized. TFBMiner also has an option for predicting TFBs that regulate single genes, rather than genes encoding enzymatic chains.

## Usage
```sh
py -m TFBMiner [-h] [-l L] [-s S] [-g G] [-o O] compound
```

## Options
`compound`: The KEGG COMPOUND database ID of the compound to predict TFBs for.

`-l, --length`: Specify the maximum integer length of the enzymatic chains to generate. Default = 3

`-s, --single_gene_operons`: Specify whether to predict biosensors for genes that encode single enzyme metabolizers, rather than genes encoding enzymatic chains (y/n). Default = n

`-g, --genome_files_path`: Specify the absolute path of the `genome_files` directory, in which the downloaded feature table bacterial genomes will be located. Otherwise, TFBMiner will try to locate it within the user's home directory.

`-o, --output_path`: Specify the absolute path of the desired output directory. Otherwise, TFBMiner will output the results to the user's home directory.

`-h, --help`: Display the software usage, description, options, and guidance in the terminal.

## Installation
These are beginner's instructions for using TFBMiner. 

### Dependencies
* Anaconda or miniconda  
Download minicoda you do not have either of these installed already
https://docs.conda.io/en/latest/miniconda.html

### Windows
Open the Anaconda/miniconda Prompt

### Linux
Open a terminal

### Create a virtual environment
Create a virtual environment using the following command  (for this part it doesn't matter where you are in your file system). If it asks if you want to proceed press y.
> conda create --name tfbMiner python=3.10

Activate the environment using the following command. You should see **(base)** on the left of the conda prompt be replaced with **(tfbMiner)**, as shown below. **If this does not happen then software that you install could affect the rest of your computer.**
> **(base)** C:\Users\ruths>conda activate tfbMiner  
**(tfbMiner)** C:\Users\ruths>

Install the requirements with the following commands 
> conda install pip  
conda install tqdm=4.62.3  
conda install numpy=1.21.5  
conda install pandas=1.5.2

### Download the code/data
Install the code by going to the github page and clicking Code, Download ZIP. Unzip the zip-file in the directory that you want to work in https://github.com/RuthStoney/TFBMiner - this will be changed to https://github.com/UoMMIB/TFBMiner onces everything's totally finalized

Download the genome files by going to the Dropbox page and clicking download (2GB of space required). Make a folder called genome_files in the directory that you want to work in (e.g. `C:\Users\ruth\TFBMiner\genome_files\`) and extract the data into there.  
https://www.dropbox.com/sh/ezo6ahj033cev8b/AADm-bC728rD0l9PTgPA9bgpa?dl=0

### Final steps before running the code
Make a results folder in the directory that you want to work in (e.g. `C:\Users\ruth\TFBMiner\results\`).

Within the conda prompt you need to us the "cd" (change directory) command to get to the correct place within your file system.
> cd (dont press enter yet!)

Open a windows explorer and drag the TFBMiner-main file into the prompt, it should look like this
> (tfbMiner) C:\Users>cd C:\Users\ruth\TFBMiner\TFBMiner-main (press enter)

Double check that you are in the `TFBMiner-main` folder and the `tfbMiner` environment. The left of your terminal should look something like this:
> **(tfbMiner)** C:\Users\ruth\TFBMiner\\**TFBMiner-main**>

### Run the code! 
Use the `-g` flag to indictate the genome data and the `-o` file to indicate the results folder that you made
> python -m TFBMiner C00259 -g C:\Users\ruth\TFBMiner\genome_files\ -o C:\Users\ruth\TFBMiner\results\

### Trouble shooting
* It didn't work - make sure that you are in the correct location within your file system by checking the file path on the left of the Anaconda prompt. The last folder should be TFBMiner.

* It returned 0 potential biosensors - Either a biosensor does not exist, or it couldn't find the genome_files. Did you put a slash at the end of your file paths? Double check the filepath provided and that you are running the code from the TFBMiner-main folder (see previous help point).


## Examples
```sh 
py -m TFBMiner C00259 -l 3
```
* Predicts TFBs for L-arabinose (ID: `C00259`)
* Identified chains will be up to `3` enzymes in length
* Nothing specified for `-g`, so TFBMiner will default to using the user's home path to find the `genome_files` directory
* Nothing specified for `-o`, so TFBMiner will default to using the user's home path and as a place to store the predictions

```sh
py -m TFBMiner C01494 -l 5 -g C:\Users\user\Desktop\genome_files -o C:\Users\user\Documents\Results
```
* Predicts TFBs for ferulic acid (ID: `C01494`) 
* Identified chains will be up to `5` enzymes in length
* Feature table genomes will be accessed via `C:\Users\user\Desktop\genome_files` (Windows OS)
* Predictions will be output to `C:\Users\user\Documents\Results` (Windows OS)

```sh
py -m TFBMiner C00180 -s y -o /Users/user/Desktop/Results
```
* Predicts TFBs for benzoate (ID: `C00180`)
* Genes that encode single enzyme metabolizers of benzoate will be used to predict TFBs
* Nothing specified for `-g`, so TFBMiner will default to using the user's home path to find the `genome_files` directory.
* Predictions will be output to `/Users/user/Desktop/Results` (Mac OS X)


## Author
Tariq Joosab & Dr Ruth Stoney

## Acknowledgements
Research supervisors: Dr Erik Hanko & Prof Rainer Breitling.
