.. _sec-interfaces-ase:

###################################
Atomic Simulation Environment - ASE
###################################

The Atomic Simulation Environment - ASE is a set of Python based tools and 
modules for setting up, manipulating, running, visualizing and analyzing 
atomistic simulations (cf. `ASE documentation 
<https://wiki.fysik.dtu.dk/ase/>`_). 

Thanks to mutual support of the `i-PI <http://ipi-code.org/>`_
socket-communication and also file-IO by ASE and DFTB+, you can freely choose
the most suitable type of communication for you. Further information can be
found in the sections linked below.

Note: Before going through the following sections, please make sure that you have 
installed a working version of the ASE package. If you are wondering how to 
`install ASE <https://wiki.fysik.dtu.dk/ase/install.html>`_, please consult the 
appropriate documentation.

.. toctree::
   :maxdepth: 1

   fileio/fileio.rst
   sockets/sockets.rst
   neb/index.rst
