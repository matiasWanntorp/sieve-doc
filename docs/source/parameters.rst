Parameters
==========

To get a quick overview of all available command line options, run:

.. code-block:: bash
   nextflow run LascauxZelia/sieve --help

Input/output options
--------------------

--data_dir 

--resultsDir (required)

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

--cat_taxonomy (required)

Run options
-----------

--file_name (default: accessions.csv) 

--page_size (default: 250)

--help or --h 

--cpus (default: 1)

--python3 (default: /opt/conda/envs/sieve/bin/python3) 

Nextflow options
----------------

-with-singulairty (default: sieve.sif) (required)

-resume




