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
interatomic potential codes, using them to calculate forces and energies under
its control. It now includes a range of advanced dynamics and structural
drivers. These include ::

  * Closed and open path integration to calculate quantum nuclear positions and
    dynamics
  * Thermodynamic integration, replica exchange and umbrella sampling to
    efficiently calculate free energies and sample free energy landscapes
  * Geometry optimisation and transition state search methods

To use i-PI you will require ::

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
--------------

The i-PI code requires a control file writen in XML, `input.xml`, along with the
specific input file for the code it is driving. Depending on the calculation,
i-PI can drive multiple separate instances of a code, hence allowing for
parallel execution. This is particularly important for cases where there are
multiple coupled structures.

DFTB+ requirements
~~~~~~~~~~~~~~~~~~

The DFTB+ binary must be compiled with the socket interface enabled. Edit
`make.config` to set ::

  WITH_SOCKETS := 1

before compiling the code.

On starting, DFTB+ will read the usual `dftb_in.hsd` file, before connecting to
an i-PI server. The `dftb_in.hsd` file should contain the usual components of
the DFTB+ input, including an initial geometry (which is used to assign the type
of boundary conditions and chemical species to each atom).

In order to be externally controlled, the `Driver {}` for DFTB+ should be set to
receive commands. This can either be via a designated file in the `/tmp/`
directory of your machine (used for the examples here) or by connecting to a
specified IP address and port number. The file based communication looks like ::
  
  Driver = Socket {
    Protocol = i-PI {} # i-PI interface
    MaxSteps = -1 # run until terminated
  }

The method and location of the communication given in `dftb_in.hsd` should of
course match the choice made in the i-PI `input.xml` file.

Quantum atomic dynamics
~~~~~~~~~~~~~~~~~~~~~~~

Path integral molecular dynamics can be used to sample quantum behaviour at
finite temperatures. It relies on the equivalence between the thermal ensemble
behavior of a set of connected classical systems and the quantum behaviour of a
single system.

If the classical systems are coupled as `ring polymers`, this allows the
determination of equilibrium properties, such as the average location and
distribution around that site. The i-PI code samples the quantum mechanics as
distinguishable particles, hence 

Replica exchange
~~~~~~~~~~~~~~~~

Standard molecular dynamics can have trouble fully exploring complex energy
landscapes in a reasonable computaional time. Hence this may not be efficient
for calculating properties such as ensemble averages.

Replica exchange instead samples the system by using several coupled systems at
different temperatures, where replicas can exchange temperatures. This allows
the system to more rapidly explore the free energy landscape by surmounting
barriers which would prevent ergodic behaviour for low temperature sampling,
while also retaining the details of the landscape at low temperatures.

NEB for barriers
~~~~~~~~~~~~~~~~

[Input: `recipes/externaldrivers/iPI_NEB`]



References
~~~~~~~~~~

.. [iPI2] i-PI 2.0: A universal force engine for advanced molecular
           simulations, V. Kapil et al. Computer Physics Communications (2018)
           DOI: `10.1016/j.cpc.2018.09.020
           <https://doi.org/10.1016/j.cpc.2018.09.020>`_
