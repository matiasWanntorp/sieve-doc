Usage
=====

Local data input
----------------

Alternatively, to use you own local data you can specify a CSV samplesheet input file that contains the paths to your FASTQ files and additional metadata. 

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

   Please provide the biome lineage correctly as same nomenlature a MGnify. If you don't know the biome lineage you can find it on the MGnify website (browse biomes data)

https://www.ebi.ac.uk/metagenomics/browse/biomes/

.. NOTE::

   A sample sheet template is available on the GitHub repository

MGnify API input
----------------

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

