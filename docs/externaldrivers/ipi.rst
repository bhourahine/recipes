*************************************
Path integrals and parallel tempering
*************************************

In this recipe, the `i-PI <http://ipi-code.org/>`_ will be used to perform some
advanced types of molecular dynamics simulations with DFTB+, using i-PI to
externally control the DFTB+ simulations.

i-PI
~~~~

Originally designed for path-integral molecular dynamics, i-PI [iPI2]_ is a
python based program which can communicate with various electronic structure and
interatomic potential codes.

You will require ::

  * Version 2.0 of i-PI
  * Python version 2.6 or later
  * the NumPy library

Firstly download or clone a copy of the `i-PI code
<http://ipi-code.org/download/>`_

Details of testing and installing i-PI are available `online
<http://ipi-code.org/resources/getting_started/>`_, in the `README.rst` file in
the i-PI repository and the `manual
<http://ipi-code.org/assets/pdf/manual.pdf>`_ included with the source code.

For simplicity we will make a local install of i-PI. In the top directory of the
i-PI code issue the following command ::
  
  python setup.py install --user

This will install the `i-pi` binary in your `~/.local/bin/` directory. If this
 path is included in your shell, you should then be able to type ::

  i-pi --help

and receive a short description of the code.

Input for i-PI
~~~~~~~~~~~~~~

The i-PI code requires a control file writen in XML, along with the specific
input file for the code it is driving. Depending on calculations, i-PI can drive
multiple separate instances of the code, hence allowing for parallel execution.

DFTB+ requirements
------------------

The DFTB+ binary must be compiled with the socket interface enabled. Edit
`make.config` and set ::

  WITH_SOCKETS := 1

before compiling the code.

On starting, DFTB+ will also read the usual `dftb_in.hsd` file, before
connecting to the i-PI server. This file should contain the usual components of
the DFTB+ input, including an initial geometry (which is used to assign the
boundary conditions and chemical types to each atom).

In order to be externally controlled, the `Driver {}` should be set to receive
commands externally. This can either be via a designated file in the `/tmp/`
directory, or to a specified machine address. For this set of recipes the local
machine address will be used ::
  
  Driver = Socket {
    Host = '127.0.0.1' # local host, ommit this to communicate via /tmp/
    Protocol = i-PI {} # i-PI interface
    MaxSteps = -1 # run until terminated
  }

The method and location of the communication should match the choice in the i-PI
input file.
  
Quantum dynamics
~~~~~~~~~~~~~~~~

Path integral molecular dynamics

Replica exchange
~~~~~~~~~~~~~~~~

Parallel tempering 

References
~~~~~~~~~~

.. [iPI2] i-PI 2.0: A universal force engine for advanced molecular
           simulations, V. Kapil et al. Computer Physics Communications (2018)
           DOI: `10.1016/j.cpc.2018.09.020
           <https://doi.org/10.1016/j.cpc.2018.09.020>`_
