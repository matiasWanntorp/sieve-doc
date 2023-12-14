Introduction
============

** `SIEVE <https://github.com/LascauxZelia/sieve>`_ ** is a bioinformatics filters-analysis pipeline for assembly, binning and annotation of metagenomes from EBI public database or local user data. 

Pipeline summary
----------------



The pipeline then:

* Check the presence of genes of interest using `diamond <https://github.com/bbuchfink/diamond>`_ 
* Performs assembly using `MEGAHIT <https://github.com/voutcn/megahit>`_ and predicts proteins-coding genes for the assemblies using `Prodigal https://github.com/hyattpd/Prodigalt>`_ .
* Check the presence of secretion systems with `MacSyFinder <https://github.com/gem-pasteur/macsyfinder>`_ .
* Extract contigs of interest with `seqtk <https://github.com/lh3/seqtk>`_ and assigns taxonomy using `CAT <https://github.com/dutilh/CAT>`_ .
* Performs metagenome binning using `MaxBin2 <https://sourceforge.net/projects/maxbin2/>`_ and `CONCOCT <https://github.com/BinPro/CONCOCT>`_ and checks the quality of the genome bins using `miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ 
* Refines bins with `DAS Tool <https://github.com/cmks/DAS_Tool>`_ 
* Assigns taxonomy to bins using `BAT <https://github.com/dutilh/CAT>`_ 

Futhermore, the pipeline creates various reports in the results directory specified, including a final table summarizing the main findings of the run.
A shiny app is available to visualise the main results. 

.. WARNING::

   The 'local data' input option only works with short reads. 

Basic usage
-----------

.. NOTE::

   If you are new to Nextflow, please refer to this `page <https://www.nextflow.io/docs/latest/getstarted.html>`_ on how to set-up Nextflow. 

.. code-block:: console

   nextflow run main.nf -with-singularity sieve.sif --resultsDir <OUTDIR> --genes <PATH/TO/GENES.fasta> --cat_db <PATH/TO/CAT_database> --cat_taxonomy <PATH/TO/CAT_taxonomy>

.. WARNING::

   Please provide pipeline parameters via the command line or Nextflow config file ``nextflow.config``.

For more details and further functionality, please refer to the usage documentation and the parameter documentation. 

Pipeline output
---------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']


API and local data
------------------


Credits
-------



Citation
--------
