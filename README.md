# Protocol for Simulations of PEGylated Proteins with Martini 3 (Tutorial Files)
This repository comprises all input files required to run our [tutorial](https://link.springer.com/protocol/10.1007/978-1-0716-0892-0_18) on simulating PEGylated proteins. 

## Abstract
Enhancement of proteins by PEGylation is an active area of research. However, the interactions between polymer and protein are far from fully understood. To gain a better insight into these interactions or even make predictions, molecular dynamics (MD) simulations can be applied to study specific protein-polymer systems at molecular level detail. Here we present instructions on how to simulate PEGylated proteins using the latest iteration of the Martini coarse-grained (CG) force-field. CG MD simulations offer near atomistic information and at the same time allow to study complex biological systems over longer time and length scales than fully atomistic-level simulations.

## Usage Notes
 - run the commands within the downloaded directory
 - if you run on MacOS or Windows you need to adjust the shell commands
 - the protocol is unfortunetly out of date with the current version of polyply.
 
## PEGylating Proteins with polyply > v1.2
In order to PEGylate the protein as in the chapter example, we first need to generate the complete residue graph of the PEGylated protein. This is done by the following command:
```
polyply gen_seq -f molecule_0.itp -from_file protein:molecule_0\
                           -from_string linker:1:1:MEE-1.0 polymer:50:1:PEO-1.0 end:1:1:OHend-1.0\
                           -seq protein linker polymer end\
                           -connects 0:1:0-0 1:2:0-0 2:3:49-0\
                           -o sequence.json -name test\
                           -label 0:"from_itp":"molecule_0-1."
```
See an in depth explanation of this command [here](https://github.com/marrink-lab/polyply_1.0/discussions/261). However, it should work to simply use it for any protein that is generated with martinize2 provided the itp file has the name `molecule_0.itp`. Next we generate the itp file of the combined molecule in one go:
```
polyply gen_itp -f molecule_0.itp MEE.itp combined_links.ff PEO.martini.3b.itp .OH_end.itp -seqf sequence.json -o lysoPEG.itp -name lysoPEG
```
If you experience any problems, have questions, or need advice on your molecule simply create a new discussion thread [here](https://github.com/marrink-lab/polyply_1.0/discussions) or post under the [old one](https://github.com/marrink-lab/polyply_1.0/discussions/261).

## Citation
```
@incollection{grunewaldprotocol,
  title={Protocol for Simulations of PEGylated Proteins with Martini 3},
  author={Gr{\"u}newald, Fabian and Kroon, Peter C and Souza, Paulo CT and Marrink, Siewert J},
  booktitle={Structural Genomics},
  pages={315--335},
  publisher={Springer}
}
```
