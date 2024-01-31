Usage
=====

MGnify API input
----------------

To use data from MGnify API you can first specify a sample accession, study accesion, experiment type, pipeline version, instrument platform, instrument model and biome name. Valid examples could look like the following:

.. code-block:: console

   --sample_accession ERR2136697
   --study_accession MGYS00001946
   --experiment_type metagenomic
   --pipeline_version 2.0
   --instrument_platform Illumina
   --instrument_model Illumina MiSeq
   --biome_name aquatic

For more details please refer to the :doc:`usage <parameters>` documentation. 

You can apply taxonomy filters on these data before the downloading step. You can specify taxonomy filters at each taxonomic level directly in the command line. 
Valid examples could look like the following:

.. code-block:: console

   --taxonomy_phylum proteobacteria
   --taxonomy_class alphaproteobacteria
   --taxonomy_order ['legionellales','triotrichales']
   --taxonomy_family legionellaceae
   --taxonomy_genus legionella
   --taxonomy_species 'legionella pneumophila'

For more details please refer to the :doc:`usage <parameters>` documentation. 

Local data input
----------------

To use you own local data you can specify a CSV samplesheet input file that contains the paths to your FASTQ files and additional metadata. 

At a minimum CSV file should contain the following columns:
sample,read_1,read_2,experiment,biome

The path to read_2 is optional. Valid examples could look like the following:

.. code-block:: console

   sample,read_1,read_2,biome
   sample1,data/sample1_R1.fastq.gz,data/sample1_R2.fastq.gz,root:Environmental:Terrestrial:Soil:Mine
   sample2,data/sample2_R1.fastq.gz,data/sample2_R2.fastq.gz,root:Environmental:Terrestrial:Soil
   sample3,data/sample3_R1.fastq.gz,data/sample3_R2.fastq.gz,root:Environmental:Terrestrial:Soil:Cave

or

.. code-block:: console

   sample,read_1,read_2,biome
   sample1,data/sample1.fastq.gz,,root:Environmental:Terrestrial:Soil:Mine
   sample2,data/sample2.fastq.gz,,root:Environmental:Terrestrial
   sample3,data/sample3.fastq.gz,,root:Environmental:Terrestrial:Soil:Cave


Please note the following requirements:

    *a minimum 4 of comma-seperated columns
    *Valid file extension: .csv
    *Must contain the header sample,read_1,read_2,biome
    *FastQ files must be compressed (.fastq.gz, .fq.gz)
    *Within one samplesheet either only single-end, assembled reads, or only paired-end reads can be specified
    *If single-end reads are specified, the command line parameter --single_end must be specified as well
    *If assembled reads are specified, the command line parameter --assembly_input must be specified as well

.. WARNING::

   Please provide the biome lineage correctly as same nomenlature a MGnify. If you don't know the biome lineage you can find it on the `MGnify website (browse biomes data) <https://www.ebi.ac.uk/metagenomics/browse/biomes/>`_

.. NOTE::

   A sample sheet template is available on the GitHub repository.

Binning
-------




