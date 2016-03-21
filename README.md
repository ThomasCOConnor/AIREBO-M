# IMPORTANT NOTE:
AIREBO-M is now part of the main LAMMPS distribution, as part of the airebo pair_style. I encourage anyone who wants to use AIREBO-M in LAMMPS to use this version, as it is maintained and updated with all the most recent LAMMPS updates and bugfixes. I plan to maintain this repository as reliable location for airebo-m parameter files.

-Thomas C. O'Connor (3.21.2016)

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

Using AIREBO-M in LAMMPS is identical to using [AIREBO](http://lammps.sandia.gov/doc/pair_airebo.html), with one important exception. AIREBO-M takes an additional 3rd flag in the pair_style command:
```
pair_style        style cutoff LJ_flag TORSION_flag REBO_flag
```
- cutoff = Long range cutoff of Morse potentials
- LJ_flag = switches on/off the Morse potentials
- TORSION_flag = switches on/off the AIREBO torsion energies
- REBO_flag = switches on/off the covalent REBO2 energies

A typical implementation in a LAMMPS script would be:
```
pair_style        airebo_morse 3.0 1 1 1
pair_coeff        * * CH.airebo-m C H
```
**Note**: The AIREBO-M Morse potentials were parameterized using a cutoff of 3.0 (sigma). Modifying this cutoff may effect simulation accuracy.

The **REBO_flag** is included so that the Morse potentials can be used with other implementations of the REBO2 covalent interactions. For example, one can use the REBO_flag to disable the REBO2 term of AIREBO-M, and use *pair_style hybrid/overlay* replace it with the bond-screening version (**REBO2Scr**) of [Pastewka et al., Phys. Rev. B 78, 161402 (2008)](http://journals.aps.org/prb/abstract/10.1103/PhysRevB.78.161402). We've recently used this hybrid technique to produce good quality results for polyethylene crystals in  [ACS Macro Lett., 2016, 5, pp 263–267](http://pubs.acs.org/doi/abs/10.1021/acsmacrolett.5b00838)
```
pair_style        hybrid/overlay atomistica Rebo2Scr airebo_morse 3.0 1 1 0
pair_coeff        * * atomistica C H
pair_coeff        * * airebo_morse CH.airebo-m C H
```

(**REBO2Scr** can be implemented in LAMMPS via the [Atomistica repository](https://github.com/Atomistica/atomistica).)

##Compatibility
AIREBO-M has been succesfully compiled in **lammps-15Jan16**.

