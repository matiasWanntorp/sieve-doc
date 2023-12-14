Installation
============

Installation instructions for sieve. 

Nextflow
--------

To run sieve, you will need to install `Nextflow <https://www.nextflow.io/docs/latest/index.html>`_ , a pipeline execution framework. Nextflow is distributed as a self-installing package, which means that it does not require any special installation procedure.

It only needs two easy steps:

    1. Download the executable package by copying and pasting either one of the following commands in your terminal window: ``wget -qO- https://get.nextflow.io | bash``

    Or, if you prefer curl: ``curl -s https://get.nextflow.io | bash``

    This will create the nextflow main executable file in the current directory.

    2. Make the binary executable on your system by running ``chmod +x nextflow``.

    3. Optionally, move the nextflow file to a directory accessible by your``$PATH`` variable (this is only required to avoid remembering and typing the full path to nextflow each time you need to run it).


Singularity
-----------

We provide a singularity container with all necessary tools installed and configured. To use it, you first need to install `Singularity <https://docs.sylabs.io/guides/3.0/user-guide/index.html>`_  itself: 

.. code-block:: bash

   $ export VERSION=3.0.3 && # adjust this as necessary \
       mkdir -p $GOPATH/src/github.com/sylabs && \
       cd $GOPATH/src/github.com/sylabs && \
       wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
       tar -xzf singularity-${VERSION}.tar.gz && \
       cd ./singularity && \
       ./mconfig

Singularity uses a custom build system called makeit. mconfig is called to generate a Makefile and then make is used to compile and install.

.. code-block:: bash

   $ ./mconfig && \
    make -C ./builddir && \
    sudo make -C ./builddir install

By default Singularity will be installed in the /usr/local directory hierarchy. You can specify a custom directory with the --prefix option, to mconfig like so:

.. code-block:: bash

   $ ./mconfig --prefix=/opt/singularity

You can also install singularity using Go.


.. WARNING::

   Install these dependencies with apt-get or yum/rpm as shown below or similar with other package managers.
   .. code-block:: bash
      $ sudo apt-get update && sudo apt-get install -y \
    build-essential \
    libssl-dev \
    uuid-dev \
    libgpgme11-dev \
    squashfs-tools \
    libseccomp-dev \
    pkg-config


Singularity container
---------------------

Then, download the container from singularity-hub or build it locally with the singularity recipe:








