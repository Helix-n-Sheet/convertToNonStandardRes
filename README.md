# ConvertToNonStandardRes
Prepare a protein model with a non-standard residue. 

# Origin for this small project: 
A post in r/bioinformatics asked the question of how they can model a protein structure with a non-standard amino acid (NSAA) in its sequence while using AlphaFold (via CollabFold). As far as I know, this is not possible since NSAAs are not included in the DL model that AlphaFold utilizes to infer protein structure from the sequence and MSA input features. Instead, I suggested they model the wild-type protein sequence in AlphaFold and then transmogrify the standard amino acid into the desired NSAA. Caveat: This can easily be done if and only if the NSAA has molecular mechanics force field topology and parameters publicly available. Once the wild-type protein structure has been converted to having the NSAA, then the interested party will need to do some visualization and structural analysis to ensure that the modification has not invalidated the AlphaFold inferred model quality. I will leave this final step for the user of this code to perform. 

Link to the reddit post: [(https://www.reddit.com/r/bioinformatics/comments/14q0gxi/how_to_put_hydroxyproline_in_alphafold_structure/)](https://www.reddit.com/r/bioinformatics/comments/14q0gxi/how_to_put_hydroxyproline_in_alphafold_structure/)

# Code Outline:
1. Gather user-defined input. Specifically, the code needs to know the residue number associated with the residue that will be modified as well as the three letter string for the new residue name. Also, point the code to the starting wild-type structure produced from AlphaFold. 
2. Read the wild-type structure into MDAnalysis, alter the ResidueGroup information for the residue of interest so that the resname is the NSAA resname. Remove most atoms associated with the wild-type residue since there may be instances where the modification is drastic. 
3. Write this temporary incomplete protein structure to file. For data provenance purposes as well as input to the next step.
4. Fix the modified protein structure by adding missing atoms, including hydrogen atoms. This step can be done in many different ways; the example provided here utilizes the ``tleap`` software from AmberTools23 package (see required packages section). This process creates ``tleap.in`` and ``leap.log`` files that increase the data provenance of this work. Keep them around.
5. Write the final modified protein structure to file. Bing-bang-boom, the structure is ready for further analysis. Check the script's work and perform post-analysis to ensure that nothing is screwed up. 

# Package Requirements:
[AmberTools23](http://ambermd.org/GetAmber.php) or really any recent version of AmberTools.
[MDAnalysis](https://docs.mdanalysis.org/stable/index.html), any recent version will suffice. 

For visualization purposes in the jupyter notebook:
[py3Dmol](https://github.com/3dmol/3Dmol.js/tree/master/py3Dmol), tested with version 2.0.3.

# License:
GPL v3. 

