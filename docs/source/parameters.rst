Parameters
==========

To get a quick overview of all available command line options, run:

.. code-block:: bash
   nextflow run LascauxZelia/sieve --help

Input/output options
--------------------

--data_dir 

--resultsDir (required)
The output directory where the results will be saved. You have to use absolute paths. 


MGnify filters option
---------------------

--biome_name (default: null)

--lineage (default: null)

--experiment_type (default: null)

--study_accession (default: null)

--sample_accession (default: null)

--instrument_platform (default: null)

--instrument_model (default: null)

--pipeline version (default: null)


--taxonomyphylum (default: null)

--taxonomyclass (default: null)

--taxonomyorder (default: null)

--taxonomyfamily (default: null)

--taxonomygenus (default: null)

--taxonomyspecies (default: null)

Control for targeted genes 
--------------------------

--genes (required)

A single path to one or several local fasta files containing orthologous groups of proteins. 

.. WARNING::

   Only ``.fasta`` extension are allowed for this process. 

--skip_diamond 

Skip diamond alignement. 

--diamond_min_align_reads (default: 0)

This is an part of an if statement that checks if the number of observed alignment from diamond analysis is not greater than the specified threshold (diamond_min_align_reads). If this condition is true, it means that there are not enough alignments, and then the file will be removed and the sample will be deleted for the rest of the pipeline. 

Assembly options
----------------

--min_contig_len (default: 1000)
Minimum length of contigs to output. 

--k_step (default: 10)
MEGAHIT uses multiple k-mer strategy. Step for iteration can be set with k_step option. 

--k_min (default: 21)
MEGAHIT uses multiple k-mer strategy. Minimum k can be set with k_min option. 

Secretion system search options
-------------------------------

--skip_macsyfinder
Skip MacSyFinder process. 

--model (default: TXSS)
For each --models options the first element must be the name of family models, followed by the name of the models. Models can be already defined and available online (see `MacSyFinder documentation <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/index.html>`_ ) or models can be create by the user with a specific structure (`macsy-model package <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/package.html#structure-of-a-macsy-model-package>`_ ). 

--nbmodel (default: all)
If the name 'all' is in the list all models from the family will be searched, otherwise only cited models will be applied. 

--modelpath (default: /opt/....)
For custom model, indicate the real path of the model.

--coverage (default: 0.8)
Minimal profile coverage required in the hit alignment to allow the hit selection for system detection. 

--evalue (default: -20)
Maximal independent e-value for Hmmer hits to be selected for system detection. 

Binning options
---------------

--markers (default: 107) (Maxbin2)
Set the markerset, choose between 107 marker genes by default or 40 marker genes. See `MaxBin2 documention <https://macsyfinder.readthedocs.io/en/latest/modeler_guide/index.html>`_ .

--probthreashold (default: 0.8) (Maxbin2)
Minimum probability for EM algorithm; default 0.8). 

--chunk_size (default: 10000) (Concoct)


--overlap_size (default: 0) (Concoct)


Bin quality check and refinement options 
----------------------------------------

--score_threashold (default: 0) (DAS Tool)

--megabin_penalty (default: 0.5) (DAS Tool)

--duplicate_penalty (default: 0.6) (DAS Tool)

--completeness (default: 0.50) (miComplete)

--redundancy (default: 1.10) (miComplete)

Taxonomic profiling and annotation options
------------------------------------------

--cat_db (required)
Absolute path of the CAT database or custom database. For CAT_prepare database path for ``2021-01-07_CAT_database/``

--cat_taxonomy (required)
Absolute path of the CAT taxonomy database or custom taxonomy database. For CAT_prepare database path for ``2021-01-07_taxonomy/``


Run options
-----------

--file_name (default: accessions.csv) 
File name to store all the accession numbers

--page_size (default: 250)
MGnify API pagination size

--help or --h 
To get a quick overview of all available command line options

--cpus (default: 1)
Number of CPUs to use. 

--python3 (default: ``/opt/conda/envs/sieve/bin/python3``) 
Location of Python3. Location of the python3 executable that has all needed packages available. Should usually be ``/usr/bin/env/python3``, leave as default is using the singularity image. 

Nextflow core options
---------------------

-with-singulairty (default: sieve.sif)
To simply specify the Singularity image file from where the containers are started. Every time your script launches a process execution, Nextflow will run it into a Singulairty container created by using the specified image. 

.. WARNING::

   The sieve.sif created for the pipeline is define in the Nextflow configuration file. 

-resume
Specigy when restarting the pipeline. Nextflow will use cached results from any pipeline steps where inputs are the same, continuing from where it got to previously. 

You can also supply a run name to resume a specific run: ``-resume [run-name]``. Usse the ``nextflow log`` command to show previous run names. 



