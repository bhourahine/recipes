*********************************
Advanced MD with an external code
*********************************

Instances of DFTB+ can be controlled by external codes. In this recipe, the
`i-PI <http://ipi-code.org/>`_ will be used to perform some advanced types of
molecular dynamics simulations with DFTB+.

i-PI
====

Originally designed for path-integral molecular dynamics, i-PI is a python based
program which can communicate with various electronic structure and interatomic
potential codes.

You will require ::

  * Python version 2.6 or later
  * the NumPy library

Firstly download or clone a copy of the i-PI code from the `github repository
<https://github.com/i-pi/i-pi>`_

Details of testing and installing i-PI are available in the `README.rst` file in
the i-PI repository and its manual.

For simplicity we will make a local install of i-PI. In the top directory of the
i-PI code issue the following command ::
  
  python setup.py install --user

This will install the `i-pi` binary in your `~/.local/bin/` directory. If this
is included in your shell path, you should then be able to type ::

  i-pi --help

and receive a short description of the code.

Quantum dynamics
================

Path integral molecular dynamics

Input files
-----------

Replica exchange
================

Parallel tempering 

Input files
-----------
