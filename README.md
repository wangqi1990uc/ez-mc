# EZ-MC
Quick and easy Monte Carlo simulations

### Metropolis Criterion Monte Carlo
The acceptance criterion are determined with Metropolis Criterion:

<img src="demo/eqn/eqn1.png"/>


The step size (`nsize`) will be updated adaptively (controlled by `fsize` and `idacc`) if not specified according to ref[1]:

<img src="demo/eqn/eqn2.png"/>

*Notes*:
1. This program is heuristic - it only gives an easy demonstration with Monte Carlo simulation and might be adapted for interaction energy parameterization.
2. Pair-wise interaction[2] were used for energy calculation, which might not be ideal for current application[3].

### Usage and example
1. Build the program with `make` command in the root directory.
2. Once done, the executable (`ez-mc`) can be found in the `bin` folder. 
3. run with `./ez-mc config.cfg`, where an example input file with a protein G (PDB: 1PGB) is given below:
```
# MC steps (int)
nstep       100000000

# MC step size (float)
# if this is specified, [fsize] and [idacc], 
# which are used to calcualte step size 
# adaptively, will be igored
# nsize       1.0

# frequency to update step size (int)
fsize       1000

# ideal acceptance ratio (float)
idacc       0.5

# freqeuncy to save coordinates (int)
fsavc       1000

# freqeuncy to write log file (int)
fsavl       1000

# Input fasta sequence file (str)
fasta       1pgb.fasta

# Output file names (str)
logname     1pgb.log
psfname     1pgb.psf
dcdname     1pgb.dcd
```

Below is a short demo, where the peptide was initially built along X-axis then equilibrated after 100M steps:

<img src="demo/demo.gif" width="50%"/>

The system is gradually relaxed when examining the time evolution of energy:

<img src="demo/ener-step.png" width="50%"/>

As expected, the acceptance ratio is populated with an average value of `0.49998`, while the values of adaptive step size are fluctuating around `0.22275`.

<img src="demo/pacc-step-hist.png" width="50%"/>

### Reference
[1] Swendsen, Robert H. "How the maximum step size in Monte Carlo simulations should be adjusted." Physics Procedia 15 (2011): 81-86.

[2] Miyazawa, Sanzo, and Robert L. Jernigan. "Estimation of effective interresidue contact energies from protein crystal structures: quasi-chemical approximation." Macromolecules 18.3 (1985): 534-552.

[3] Vendruscolo, Michele, and Eytan Domany. "Pairwise contact potentials are unsuitable for protein folding." The Journal of chemical physics 109.24 (1998): 11101-11108.