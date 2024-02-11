# Alphaionic
a python script that filters Alphafill's additions to alphafold models


Downnload and extract the Alphaionic.tar.gz
You will find two python scripts:
1_filter.py
By typing the uniprot id (alfafill name, pex AF-O64637-F1, or just O64637) the script will download the cif file from afill.
This script will remove all the transplants except metals and heme
It will filter the transplants according to the confidence scores provided by afill
You can adjust the scores at line 61 for heme, lines 70-74 for metals
It will remove transplants that are close to each other an don't originate from the same entry.
You can adjust the distance at line 102 ( r[i][j]<5 ), default is 5A, 
The edited file is provided as cif, Edited+idname+.cif
Only python is required. No other file is required to run this script. You can loop this if you want to as in alphaionic.py

alphaionic.py
Needs pymol2 and gromacs installed, (on ubuntu sudo apt install pymol and sudo apt install gromacs, is enough).
Open the 0afstructures.txt file and insert as many uniprot ids or afill names you want and separate them by enter as such
AF-xxx-F1
AF-yyy-F1
run the script, python3 alphafiltered.py
Firstly it will work as the previous script
distance threshold at line 106, scores at line 75-79
Then, using pymol it will remove transplants that have high confidence scores but are not bound anywhere.
Line 141, default distance <3.4A close to S or N or O, in order not to be removed 
for heme at line 151, default 4. Heme is filtered with lrmsd at line 160. At 168 you can adjust the least distance allowed between two hemes
and at line 193, the max distance between a metal and a heme
If you can't or dont want to use gromacs for energy minimization but want to use pymol for improved filtering, comment out ## the region: 264 and below.
You can adjust minimization process on minim.mdp and gromin.sh
be sure that gromacs is ready to work, you may need to lacate it running : source /usr/local/gromacs/bin/GMXRC
You may need to REPLACE gmx with gmx_mpi in gromin.sh

This code worked in 10/2/2024, if any change in alphafill database occured before, or in gromacs or pymol, that affected the script
this script may not function properly

0afstructures is a list of human proteins with unkown structures at the moment, and a good alphafold model in a region of interest 
0existing is a list of known human protein stuctures (for comparison)
