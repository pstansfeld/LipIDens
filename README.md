# LipIDens - simulation assisted interpretation of lipid densities 

![logo](lipidens_final_Asset_2.png)

LipIDens is an open-source pipeline for simulation-assisted interpretation of lipid and lipid-like densities observed in cryo-electron microscopy (cryo-EM) structures of membrane proteins.

LipIDens integrates coarse-grained and atomistic molecular dynamics (MD) simulations with PyLipID-based analysis to identify, characterise, and rank lipid binding sites, enabling experimental densities to be connected to specific lipid chemistries. 

## Key Capabilities:
- Differentiating between sterol and phospholipid binding sites where structural densities are ambiguous. 
- Assess preferential binding of different lipid types to a site where lipid-like density is observed.
- Evaluate whether lipid tail densities are likely to belong to the same or adjacent binding sites. 
- Quantify the kinetics of different lipids binding to the same site.
- Obtain a more complete picture of lipid interactions profiles around the protein in a membrane environment. 
- Assist interpretation of cryo-EM densities during model building and map refinement cycles. 
- Assess which putative lipid binding sites may prevail when not in detergent conditions. 

## Scope of the Pipeline:
LipIDens provides workflow automation and analysis tools. The user is responsible for:

Running MD simulations (e.g. with GROMACS)
Providing trajectories and topology files
LipIDens then processes these data to guide structural interpretation.

## Installation:

For detailed instructions on LipIDens Installation please refer to the latest version, courtesy of the Stansfeld Lab, University of Warwick.

[Latest LipIDens Version and Installation](https://github.com/pstansfeld/LipIDens/), updated October 2026 (version 1.2.0)

LipIDens requires a python3 environment (**>= 3.11**). LipIDens is not on PyPI: install it from this GitHub repository.

```bash
mamba create -n lipidens python=3.12 -y
mamba activate lipidens
mamba install -c conda-forge gromacs pdb2pqr -y
pip install git+https://github.com/pstansfeld/LipIDens.git
```

This installs LipIDens with its Python dependencies, including [PyLipID](https://github.com/pstansfeld/PyLipID) (>= 1.6) and [vermouth](https://github.com/marrink-lab/vermouth-martinize) (`martinize2`), together with the workflow scripts and parameter files it uses. See [README_INSTALL.md](README_INSTALL.md) for installing from a clone.

For the atomistic stages (backmapping lipid poses in stage 5 and setting up atomistic simulations in stage 6) also install [cg2at-lite](https://github.com/pstansfeld/cg2at-lite) (`pip install cg2at-lite`); the original [CG2AT](https://github.com/owenvickery/cg2at) is used instead if cg2at-lite is not installed. Comparing poses with densities (stage 5) writes a [PyMOL](https://pymol.org) script.

#### Running LipIDens

Run the protocol interactively, stage by stage (1a/1b: coarse-grained setup and processing, 2: test PyLipID cut-offs, 3: run PyLipID, 4: screen PyLipID data, 5: rank site lipids, 6: atomistic setup):

```bash
lipidens
```

(or `python lipidens_master_run.py` from a clone of this repository), or follow the [LipIDens workflow notebook](LipIDens.ipynb).

If you write your own scripts that call LipIDens or PyLipID, put the code under `if __name__ == "__main__":`: PyLipID calculates in worker processes that re-import the script.

Note: from version 1.2.0 the number of homomeric protein chains (`nprot`) is passed through to PyLipID (it was previously fixed at 1), so results for homomers can differ from those of earlier versions.

## Citation:

**Please cite** the following if you use LipIDens in your research:

Ansell, T.B., Song, W., Coupland, C.E., Carrique, L., Corey, R.A., Duncan, A.L., Cassidy, C.K., Geurts, M.M.G., Rasmussen, T., Ward, A.B., Siebold, C., Stansfeld, P., Sansom, M.S.P. (2023). **LipIDens: Simulation assisted interpretation of lipid densities in cryo-EM structures of membrane proteins.** Nature Communications 14, 7774, [doi: 10.1038/s41467-023-43392-y](https://www.nature.com/articles/s41467-023-43392-y)

**Accompanying step by step protocol** citation:

Ansell, T.B., Song, W., Coupland, C.E., Carrique, L., Corey, R.A., Duncan, A.L., Cassidy, C.K., Geurts, M.M.G., Rasmussen, T., Ward, A.B., Siebold, C., Stansfeld, P., Sansom, M.S.P. (2023). **Implementation of the LipIDens pipeline: assisted interpretation of lipid densities in membrane protein structures using simulations.** protocols exchange, [doi: 10.21203/rs.3.pex-2408/v1](https://doi.org/10.21203/rs.3.pex-2408/v1)

The LipIDens logo was designed by Jessica Ansell. 

## Legacy Installation (OLD):

See above for latest installation of LipIDens. The instructions below are for the original version (1.0.0) in [TBGAnsell/LipIDens](https://github.com/TBGAnsell/LipIDens) (Python 3.9, PyLipID 1.5).

LipIDens installation from the GitHub repository:
```bash
git clone https://github.com/TBGAnsell/LipIDens
cd LipIDens
python setup.py install
```

#### Recomended

Recommended to use dssp version 3 as this is the only current version compatible with martinize2. Check your version using `mkdssp --version`. (Not needed for the latest version: current martinize2 assigns secondary structure with mdtraj.)

```bash
conda install -c salilab dssp
```


Conda (legacy installation):
```bash
conda create -n LipIDens python=3.9
pip install -r requirements.txt
```
