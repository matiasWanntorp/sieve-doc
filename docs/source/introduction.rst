Introduction
============

`SIEVE <https://github.com/LascauxZelia/sieve>`_ is a bioinformatics filters-analysis pipeline for assembly, binning and annotation of metagenomes from EBI public database or local user data. 

Pipeline summary
----------------



The pipeline then:

* Check the presence of genes of interest using `diamond <https://github.com/bbuchfink/diamond>`_ 
* Performs assembly using `MEGAHIT <https://github.com/voutcn/megahit>`_ and predicts proteins-coding genes for the assemblies using `Prodigal <https://github.com/hyattpd/Prodigalt>`_ .
* Check the presence of secretion systems with `MacSyFinder <https://github.com/gem-pasteur/macsyfinder>`_ .
* Extract contigs of interest with `seqtk <https://github.com/lh3/seqtk>`_ and assigns taxonomy using `CAT <https://github.com/dutilh/CAT>`_ .
* Performs metagenome binning using `MaxBin2 <https://sourceforge.net/projects/maxbin2/>`_ and `CONCOCT <https://github.com/BinPro/CONCOCT>`_ and checks the quality of the genome bins using `miComplete <https://bitbucket.org/evolegiolab/micomplete/src/master/>`_ 
* Refines bins with `DAS Tool <https://github.com/cmks/DAS_Tool>`_ 
* Assigns taxonomy to bins using `BAT <https://github.com/dutilh/CAT>`_ 

Futhermore, the pipeline creates various reports in the results directory specified, including a final table summarizing the main findings of the run.
A shiny app is available to visualise the main results. 

Basic usage
-----------

.. NOTE::

   If you are new to Nextflow, please refer to this `page <https://www.nextflow.io/docs/latest/getstarted.html>`_ on how to set-up Nextflow. 

.. code-block:: console

   nextflow run main.nf -with-singularity sieve.sif --resultsDir <OUTDIR> --genes <PATH/TO/GENES.fasta> --cat_db <PATH/TO/CAT_database> --cat_taxonomy <PATH/TO/CAT_taxonomy>

.. WARNING::

   Please provide pipeline parameters via the command line or Nextflow config file ``nextflow.config``.

For more details and further functionality, please refer to the :doc:`usage <usage>` documentation and the :doc:`parameter <parameters>` documentation. 

Pipeline output
---------------

To see the results of an example test run with a full size dataset refers to results tab on the Github pipeline page. For more details about the output files and reports, please refer to the :doc:`output <output>` documentation.


Inputs
------

Two types of input are supported by the pipeline. 

Local data
~~~~~~~~~~


.. WARNING::

   The 'local data' input option only works with short reads. 

MGnify API
~~~~~~~~~~



For more details, please refer to the :doc: `input <input>` documentation. 

Credits
-------

SIEVE pipeline was written by Zelia Bontemps, Andrei Gullaiev and Lionel Guy at Uppsala University (Departement of Medical Biochemistry and Microbiology.

We thank the MGnify team for the assistance in the developpement of this pipeline. 


Citation
--------

If you use SIEVE, please cite the article: 


