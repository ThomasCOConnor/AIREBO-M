# AIREBO-M
This repository contains source files for the [LAMMPS](http://lammps.sandia.gov) implementation of the **AIREBO-M** reactive bond order potential for hydrocarbons, described in [O'Connor et al., J. Chem. Phys. 142, 024903 (2015)](http://scitation.aip.org/content/aip/journal/jcp/142/2/10.1063/1.4905549).

AIREBO-M is a modified version of the the AIREBO potential described in [Stuart et al., J. Chem. Phys. 112, 6472 (2000)](http://scitation.aip.org/content/aip/journal/jcp/112/14/10.1063/1.481208). AIREBO-M replaces the Lennard-Jones potentials of AIREBO's van der Waal's interactions with Morse potentials. The Morse potentials are parameterized by high-quality quantum chemistry (MP2) calculations. The Morse potentials, which do not diverge as particle density increases, allow AIREBO-M to retain accuracy to much higher pressures than AIREBO (up to 40 GPa for Polyethylene).

##Compiling With LAMMPS

Compiling AIREBO-M with LAMMPS is simple if you have already successfully compiled the default LAMMPS build which contains AIREBO. The repository contains the following files:

1. pair_airebo_morse.cpp
2. pair_airebo_morse.h
3. CH.airebo-m

Just place the .cpp and .h files in the **lammps[version]/src/** directory and compile LAMMPS. The file **CH.airebo-m** is the potential paramter file accessed by the pair_coeff command in a LAMMPS script.

##Usage in LAMMPS

Using AIREBO-M in LAMMPS is identical to using [AIREBO](http://lammps.sandia.gov/doc/pair_airebo.html), with one important exception. The **AIREBO** pair_style takes 3 arguments: cutoff, LJ_flag, TORSION_flag.
