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

--skip_diamond 
Skip diamond alignement. 

--diamond_min_align_reads (default: 0)

--genes (required)

Assembly options
----------------

--min_contig_len (default: 1000)

--k_step (default: 10)

--k_min (default: 21)

Secretion system search options
-------------------------------

--modelpath (default: /opt/....)

--model (default: TXSS)

--nbmodel (default: all)

--coverage (default: 0.8)

--evalue (default: -20)

Binning options
---------------

--markers (default: 107) (Maxbin2)

--probthreashold (default: 0.8) (Maxbin2)

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



