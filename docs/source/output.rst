Output
======

Introduction
------------

This section describes the output produced by the pipeline.

Pipeline overview
-----------------

The sieve pipeline is built using Nextflow and processes data using the following steps:

* Control of local input reads (trimming) - (Only if --local is set)
* Fetching data from MGnify API (Filters and download) - (Only if --noapi is not set)
* Identification of genes of interest on raw trimmed reads - (Only if --nodiamond is no set)
* Assembly of trimmed reads
* Proteins coding gene prediction of assemblies
* Identification of contigs that contains macromolecular systems, genetic pathways of our interest
* Taxonomic classification of the targeted contigs
* Binning and binning refinement of targeted contigs
* Genome annotation of binned genomes
* Taxonomic classification of binned genomes
* Summary
* Pipeline information - Metrics generated during the workflow execution


* Check for the presence of genes of interest using `diamond <https://github.com/bbuchfink/diamond>`_ 
* Performs assembly using `MEGAHIT <https://github.com/voutcn/megahit>`_ and predicts proteins-coding genes for the assemblies using `Prodigal <https://github.com/hyattpd/Prodigalt>`_ .
* Check for the presence of macromolecular secretion systems with `MacSyFinder <https://github.com/gem-pasteur/macsyfinder>`_ .
* Extract contigs of interest using `seqtk <https://github.com/lh3/seqtk>`_ and assigns taxonomy using `CAT <https://github.com/dutilh/CAT>`_ .
* Performs metagenome binning using `MaxBin2 <https://sourceforge.net/projects/maxbin2/>`_ and `CONCOCT <https://github.com/BinPro/CONCOCT>`_ and checks the quality of the genome bins using `miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ 
* Refines bins with `DAS Tool <https://github.com/cmks/DAS_Tool>`_ 
* Assigns taxonomy to bins using `BAT <https://github.com/dutilh/CAT>`_ 



Control of local input reads
----------------------------

Adapterremoval

`Adapterremoval <https://github.com/MikkelSchubert/adapterremoval>`_ searches for and removes remnant adapter sequences form High-throughput Sequencing (HTS) data and optionally trims low quality bases from the 3' end of reads following adapter removal. The output logs are stored in the results folder. 

Output files:
  * ``[sample]_trimSE.fastq.gz`` if --single-end is specified
  * ``[sample]_trimPE.fastq.gz`` for pair-end reads

Fetching data from MGnify API
-----------------------------

Getting accession 

Targeting taxonomy

Downloading


Identification of genes of interest
-----------------------------------

Generating diamond database
Create a DIAMOND formatted reference database from a FASTA input file.
Output files:

Identification of target genes using diamond. Diamond is a sequence aligner for protein and translated DNA searches, designed for high performance analysis of big sequence data. 
Output files:


Assembly
--------

Reads are assembled with MEGAHIT. MEGAHIT is a single node assembler for large and complex metagenomics short reads.
Output files:

Gene prediction
---------------

Protein-coding genes are predicted for each assembly using Prodigal.
Output files:

Identification of macromolecular systems
-----------------------------------------

MacSyFinder is a program to model and detect macromolecular systems, genetic pathways… in protein datasets. Criteria for systems detection include component content (quorum), and genomic co-localization. Each component corresponds to a hidden Markov model (HMM) protein profile to perform sequence similarity searches with the program Hmmer.
Output files:

Taxonomic classification of the targeted contigs
------------------------------------------------

CAT is a toolkit for annotating contigs and bins from metagenome-assembled-genomes. The sieve pipeline uses CAT to assign taxonomy to targeted contigs.
Output files:

Binning and binning refinement
------------------------------

Contig coverage
Create bwa index, Align reads with bwa mem, Convert and sort sam to bam file using samtools, Index BAM file, Output per contig coverage using pileup.sh, Generate abundance file from mapped reads
These files ares for downstream binning steps.
Output files: 


Maxbin2
MetaBAT2 recovers genome bins (that is, contigs/scaffolds that all belongs to a same organism) from metagenome assemblies.
Output files:

Concoct
CONCOCT performs unsupervised binning of metagenomic contigs by using nucleotide composition, coverage data in multiple samples and linkage data from paired end reads.
Output files:

DASTool
DAS Tool is an automated binning refinement method that integrates the results of a flexible number of binning algorithms to calculate an optimized, non-redundant set of bins from a single assembly. nf-core/mag uses this tool to attempt to further improve bins based on combining the MetaBAT2 and MaxBin2 binning output, assuming sufficient quality is met for those bins.

DAS Tool will remove contigs from bins that do not pass additional filtering criteria, and will discard redundant lower-quality output from binners that represent the same estimated ‘organism’, until the single highest quality bin is represented.

WARNING ::
  If DAS Tool does not find any bins passing your selected threshold it will exit with an error. 

Output files:


miComplete
miComplete is a compact software aimed at rapidly and accurately determining of the quality of assembled genomes, often metagenome assembled bins. miComplete also aims at providing a more reliable completeness and redundancy metric via a system of weighting the impact of different marker genes presence or absence differently.
Output files:

Genome annotation of binned genomes
-----------------------------------

Protein-coding genes are predicted for each bin that match de bins quality criteria defined by the user. 
Output file:

Taxonomic classification of binned genomes
------------------------------------------

CAT is a toolkit for annotating contigs and bins from metagenome-assembled-genomes. The sieve pipeline uses BAT to assign taxonomy to genome bins based on the taxnomy of the contigs.
Output files:

Summary
-------

Generate the general stats table and plot for the pipeline. 
Output file:

Pipeline information
--------------------


