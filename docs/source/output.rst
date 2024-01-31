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

Control of local input reads
----------------------------

Adapterremoval
~~~~~~~~~~~~~~

`Adapterremoval <https://github.com/MikkelSchubert/adapterremoval>`_ searches for and removes remnant adapter sequences form High-throughput Sequencing (HTS) data and optionally trims low quality bases from the 3' end of reads following adapter removal. The output logs are stored in the results folder. 

Output files:
  * ``[sample]_trimSE.fastq.gz`` if --single-end is specified
  * ``[sample]_trimPE.fastq.gz`` for pair-end reads

Fetching data from MGnify API
-----------------------------

Getting accession
~~~~~~~~~~~~~~~~~

Getting all analysis accession from MGnify API based on the parameters in the command line. 

Output files:
 * in ``outdir/acession/``
  * ``accession.csv``

Targeting taxonomy
~~~~~~~~~~~~~~~~~~

Apply taxonomic filters on the accession obtained previously.

Output files:
 * in ``outdir/taxonomy/``
  * ``[sample]_ID_to_download.csv``
  * ``[sample]_taxonomy_details.csv``

Downloading
~~~~~~~~~~~

Downloading data using accession number. 

Output files: 
 * ``[sample].fastq.gz``


Identification of genes of interest
-----------------------------------

Generating diamond database
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a `diamond <https://github.com/bbuchfink/diamond>`_  formatted reference database from a FASTA input file.
Output files:
  * ``references.dmnd``
  * ``references.fasta``

Identification of target genes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
`Diamond <https://github.com/bbuchfink/diamond>`_ is a sequence aligner for protein and translated DNA searches, designed for high performance analysis of big sequence data. 
Output files:
  * ``[sample].daa``

Assembly
--------

Reads are assembled with `MEGAHIT <https://github.com/voutcn/megahit>`_ . MEGAHIT is a single node assembler for large and complex metagenomics short reads.
Output files:
  * ``[sample]_assembly_MG.fasta`` if experiment type is metagenomic
  * ``[sample]_assembly_AS.fasta`` if experiment type is assembly

Gene prediction
---------------

Protein-coding genes are predicted for each assembly using `Prodigal <https://github.com/hyattpd/Prodigalt>`_ .
Output files:

* ``[sample].faa``

Identification of macromolecular systems
-----------------------------------------

`MacSyFinder <https://github.com/gem-pasteur/macsyfinder>`_  is a program to model and detect macromolecular systems, genetic pathways… in protein datasets. Criteria for systems detection include component content (quorum), and genomic co-localization. Each component corresponds to a hidden Markov model (HMM) protein profile to perform sequence similarity searches with the program Hmmer.
Output files:

* in ``<outdir>/contig/``

  * ``[sample]_contig.fasta`` 
  * ``[sample]_contig_name_deduplicated.txt``

* in work dir

 * ``[sample]_contig_names.txt``
 * ``[sample]_contig_proteins.faa.idx`` 
 * in ``out_macsyfinder``/[sample]/

  * ``all_best_solutions.tsv``

Taxonomic classification of the targeted contigs
------------------------------------------------

`CAT <https://github.com/dutilh/CAT>`_  is a toolkit for annotating contigs and bins from metagenome-assembled-genomes. The sieve pipeline uses CAT to assign taxonomy to targeted contigs.
Output files:

* in ``<outdir>/contig/classification/``

  * ``[sample]_classification_summary.txt`` 

* in work dir

  * ``[sample].alignment.diamond``
  * ``[sample].contig2classification.txt`` 
  * ``[sample].ORF2LCA.txt``
  * ``[sample]classification_names.txt`` 
  * ``[sample]classification_official_names.txt`` 
  * ``[sample].log``
  * ``[sample].predicted.proteins.faa``
  * ``[sample].predicted.proteins.gff``

Binning and binning refinement
------------------------------

Contig coverage
~~~~~~~~~~~~~~~

Create bwa index, Align reads with `bwa <https://bio-bwa.sourceforge.net>`_ mem, Convert and sort sam to bam file using `samtools <https://github.com/samtools/samtools>`_ , Index BAM file, Output per contig coverage using pileup.sh, Generate abundance file from mapped reads
These files ares for downstream binning steps.

Output files: 
 * ``[sample]_abundance.txt``
 * ``[sample]_aln.bam``
 * ``[sample]_aln.sam``
 * ``[sample]_cov.txt``
 * ``[sample]_index.amb/ann/bwt/pac/sa``

Maxbin2
~~~~~~~

`MaxBin2 <https://sourceforge.net/projects/maxbin2/>`_ recovers genome bins (that is, contigs/scaffolds that all belongs to a same organism) from metagenome assemblies.

Output files:

Concoct
~~~~~~~

`CONCOCT <https://github.com/BinPro/CONCOCT>`_ performs unsupervised binning of metagenomic contigs by using nucleotide composition, coverage data in multiple samples and linkage data from paired end reads.

Output files:
* in ``workdir/[sample]_concot_bins/``
  * ``[sample]_concoct.*.fa`` 

* in work dir

  * ``[sample]_args.txt``
  * ``[sample]_clustering_gt1000.csv`` 
  * ``[sample]_clustering_merged.csv``
  * ``[sample]_concoct.contigs2bin.tsv`` 
  * ``[sample]_contigs_10K.bed`` 
  * ``[sample]_contigs_10K.fasta`` 
  * ``[sample]_coverage_table.tsv``
  * ``[sample]_original_data_gt1000.csv``
  * ``[sample]_PCA_components_data_gt1000.csv`` 
  * ``[sample]_PCA_transformed_data_gt1000.csv`` 
  * ``[sample]_log.txt``

DASTool
~~~~~~~

`DAS Tool <https://github.com/cmks/DAS_Tool>`_ is an automated binning refinement method that integrates the results of a flexible number of binning algorithms to calculate an optimized, non-redundant set of bins from a single assembly. nf-core/mag uses this tool to attempt to further improve bins based on combining the MetaBAT2 and MaxBin2 binning output, assuming sufficient quality is met for those bins.

DAS Tool will remove contigs from bins that do not pass additional filtering criteria, and will discard redundant lower-quality output from binners that represent the same estimated ‘organism’, until the single highest quality bin is represented.

WARNING ::
  If DAS Tool does not find any bins passing your selected threshold it will exit with an error. 

Output files:


miComplete
~~~~~~~~~~

`miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ is a compact software aimed at rapidly and accurately determining of the quality of assembled genomes, often metagenome assembled bins. miComplete also aims at providing a more reliable completeness and redundancy metric via a system of weighting the impact of different marker genes presence or absence differently.

Output files:
 * ``[bin_name].fna``
 * ``[bin_name]_bins_stats_quality.tab``
 * ``micomplete.log``

Genome annotation of binned genomes
-----------------------------------

`miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ also perform the protein-coding genes prediction for each bin that match de bins quality criteria defined by the user. 

Output file:
 * ``[bin_name]_profigal.faa``

Taxonomic classification of binned genomes
------------------------------------------

`BAT <https://github.com/dutilh/CAT>`_  is a toolkit for annotating contigs and bins from metagenome-assembled-genomes. The sieve pipeline uses BAT to assign taxonomy to genome bins based on the taxnomy of the contigs.

Output files:

Summary
-------

Generate the general stats table and plot for the pipeline. 

Output file:

Pipeline information
--------------------


