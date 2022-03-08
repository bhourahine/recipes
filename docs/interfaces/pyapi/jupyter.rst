.. highlight:: none
.. _sec-interfaces-jupyter:

***************************
Use jupyter for a worksheet
***************************

For a literate worksheet, performing some calculations with DFTB+ and
then using tools like jmol to visualise the results, we can use the
`jupyter <https://jupyter.org/>`_ web interface and condaforge
packages.

Seting up the environment
=========================

Initialise and populate an environment using the condaforge DFTB+ and jupyter::

  conda create -n dftbplus
  conda activate dftbplus

  conda install jupyter notebook
  conda install dftbplus-tools dftbplus-python


Add components from pip for jupyter itself::

  pip install jupyter
  pip install jupyter_jsmol
  pip install ase pymatgen

Notebooks
=========

[Input: `recipes/interfaces/pyapi/`]

Then load a notebook for a solid state example::

  jupyter notebook recipes/interfaces/pyapi/1_ga2o3.ipynb

This sets up and solves the unperturbed ground state for a Ga2O3
crystal in a few different polytypes, then evaluates the clamped and
relaxed-ion piezoelectric tensors by finite difference. The steps of
the calculation are documented in the worksheet.

From the jupyter interface, load a molecular example::

  file -> open -> 2_C6H6.ipynb

This evaluates the excited states using two different methods (Casida
excitations and :math:`{\Delta}`-SCF) and generates a scan of the
landscape around the conical intersection between the :math:`s_{0}`
and :math:`s_{1}` surfaces.

