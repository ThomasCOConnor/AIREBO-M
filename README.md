# AIREBO-M
This repository contains source files for the **LAMMPS** implementation of the **AIREBO-M** reactive bond order potential for hydrocarbons, described in **O'Connor et al., J. Chem. Phys. 142, 024903 (2015)**.

AIREBO-M is a modified version of the the AIREBO potential described in **Stuart et al., J. Chem. Phys. 112, 6472 (2000)**. AIREBO-M replaces the Lennard-Jones potentials of AIREBO's van der Waal's interactions with Morse potentials. The Morse potentials are parameterized based on high-quality quantum chemistry (MP2) calculations. AIREBO-M extends the accuracy of AIREBO to much higher pressures (up to 40 GPa for Polyethylene).

##Compiling With LAMMPS

Compiling AIREBO-M with LAMMPS is simple if you have already successfully compiled the default LAMMPS build which contains AIREBO. The repository contains the following files:

1. pair_airebo_morse.cpp
2. pair_airebo_morse.h
3. CH.airebo-m

Just place the .cpp and .h files in the **lammps[version]/src/** directory and compile LAMMPS. The file **CH.airebo-m** is the potential paramter file accessed by the pair_coeff command in a LAMMPS script.
