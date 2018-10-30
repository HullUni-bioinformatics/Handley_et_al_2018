# Handley_et_al_2018  need to be fixed

Data processing workflow and supplementary data for Handley et al. 2018 - Temporal and spatial variation in distribution of fish environmental DNA in England’s largest lake. _bioRxiv_ DOI: ([here](http://sci-hub.tw/10.1101/376400))

Release 1.0 of this repository has been archived: 

##Contents
 - __Supplementary data__ ([here](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/tree/master/supplementary_data))
 1. reference sequences (curated reference databases) used in analyses in Genbank format ([here](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/tree/master/supplementary_data/reference_DBs))
 2. adapter sequences used for 12S fragment ([here](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/tree/master/supplementary_data/adapters))
 3. SRA accession numbers for raw Illumina data ([here](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/blob/master/supplementary_data/Sample_accessions.tsv))
 4. R scripts used to produce the figures in the paper ([here]())
 

##Instructions on how to set up all dependencies for data processing/analyses
 
To facilitate full reproducibility of our analyses we provide Jupyter notebooks illustrating our workflow and all necessary supplementary data in this repository.

Illumina data was processed (from raw reads to taxonomic assignments) using the [metaBEAT](https://github.com/HullUni-bioinformatics/metaBEAT) pipeline. The pipeline relies on a range of open bioinformatics tools, which we have wrapped up in a self contained docker image which includes all necessary dependencies [here](https://hub.docker.com/r/chrishah/metabeat/).

##Setting up the environment

In order to retrieve supplementary data (reference sequences etc.) start by cloning this repository to your current directory:
```
git clone --recursive https://github.com/HullUni-bioinformatics/Handley_et_al_2018.git
```

In order to make use of our self contained analysis environment you will have to install [Docker](https://www.docker.com/) on your computer. Docker is compatible with all major operating systems. See the [Docker documenation](https://docs.docker.com/) for details. On Ubuntu installing Docker should be as easy as:

```
sudo apt-get install docker.io
```

Once Docker is installed you can enter the environment by typing, e.g.:
```
sudo docker run -i -t --net=host --name metaBEAT -v $(pwd):/home/working chrishah/metabeat /bin/bash
```

This will download the metaBEAT image (if it's not yet present on your computer) and enter the 'container', i.e. the self contained environment (Note that `sudo` may be necessary in some cases). With the above command the container's directory `/home/working` will be mounted to your current working directory (as instructed by `$(pwd)`), in other words, anything you do in the container's `/home/working` directory will be synced with your current working directory on your local machine. 
 

##Data processing workflow as Jupyter notebooks

Raw illumina data has been deposited with Genbank (BioProject: PRJNA414952; BioSample accession: SAMN07811461-SAMN07811580; Sequence Read Archive accessions: SRR6189420-SRR6189539) - see sample specific accessions [here](https://github.com/HullUni-bioinformatics/Li_et_al_2017/blob/master/supplementary_data/Sample_accessions.tsv). Before following the workflow below, you'll need to download the raw reads from SRA. To __download the raw read data__ you can follow the steps in [this Jupyter notebook](https://github.com/HullUni-bioinformatics/Li_et_al_2017/blob/master/raw_reads/How_to_download_Rawdata_from_SRA.ipynb).


With the data in place you should be able to __fully rerun/reproduce our analyses__ by following the steps outlined in the Jupyter notebooks that we provide for the [12S](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/blob/master/12S/12S.ipynb) and [CytB](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/blob/master/CytB/CytB.ipynb) datasets.

The workflow illustrated in the notebooks assumes that the raw Illumina data is present in a directory `raw_reads` at the base of the repository structure and that the files are named according to the following convention:
'sampleID-marker', followed by '_1' or '_2' to identify the forward/reverse read file respectively. sampleID must corresponds to the first column in the file `Sample_accessions.tsv` [here](https://github.com/HullUni-bioinformatics/Haenfling_et_al_2016/blob/master/supplementary_data/Sample_accessions.tsv), marker is either '12S' or 'CytB'.

