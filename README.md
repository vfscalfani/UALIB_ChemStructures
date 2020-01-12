# UALIB_ChemStructures
Chemical Substances from The University of Alabama Dissertations and Theses

## What is this?
This repository contains the original indexed chemical substances (non-standardized) 
from The University of Alabama Dissertations and Theses (hereafter, theses). 

**At the moment, there are about 350 structures, however, we are hoping to get to > 5000 structures in 6 months, so check back!.**

Chemical structure data includes the name, SMILES, and InChI of all synthesized chemical
structures within the thesis along with a permalink to the thesis full-text or 
catalog link (if not yet available online), Moreover, an SDfile containing the connection table, name, 
SMILES, InChI, citation, permalink, and local structure registry ID is included. 
The RDKit processed SDfile is what we submit directly to PubChem. PubChem is likely where you want to download our 
data from as PubChem handles the standardization of the chemical structures:
[The University of Alabama Libraries PubChem Data Source](https://pubchem.ncbi.nlm.nih.gov/source/15645).
However, this GitHub repository is useful for those seeking to download our non-standardized data
and understand our workflow.

## How are we indexing the chemical structures?

* This is a manually curated effort, no machine extraction. 
We are redrawing and encoding the structures ourselves.

* We include only structures that can be represented with SMILES. 
Essentially this includes small molecule organic chemistry with some
limited organometallic chemical substances.

* Chemical substances indexed must have synthetic experimental characterization
details such as NMR, mass spec, elemental analysis, and melting point. 
No judgment is made on the the accuracy of the reported syntheses. 
If the authors claimed they synthesized the substance in an experimental section and
includes characterization data, we indexed it. 

* The substance name given in the dissertation is preferred and used. 
If no name is given, we generated an IUPAC name, where possible, using the NCI/CADD
Chemical Identifier Resolver.

* Duplicates are assigned the same local Registry ID (i.e., UALIB-###). We check 
for duplicates via the InChIKey, then update the original PubChem Substance record 
with the additional thesis reference.

## What is your workflow? 

We're still working on creating an optimal open workflow that is highly reproducible. Here is an overview of our current strategy:

1. Draw chemical structures in [ChemAxon MarvinSketch](https://chemaxon.com/products/marvin). We really like the free [PubChem Sketcher](https://pubchem.ncbi.nlm.nih.gov/edit3/index.html) too, however, we found it much faster to use MarvinSketch.
2. Export as Daylight ChemAxon SMILES (v19.27.0) and calculate InChIKeys (v1.05 as computed by ChemAxon molconvert v19.27.0)
3. Create a tab delimited file with an index number for each compound (i.e., UALIB-###), 
the name, citation, and permalink to the thesis. 
4. Import the tabbed text file into an RDKit Pandas dataframe to calculate the 
InChIs, InChIKeys, write kekulized SMILES, and generate the SDfile (InChIs v1.05 as computed by RDKit 2019.09.2 release).
5. Compare RDKit and ChemAxon InChIKeys (this helps catch any issues with SMILES parsing across the toolkits). If the InChIKeys do not match, we figure out the issue before adding the structure to the index.
6. Submit the SDfile to PubChem.
7. Update the UALIB_Chemical_Structures_REGID files
8. Create a record on our [Institutional Repository](https://ir.ua.edu/) with the SDfile.

## File Overview Notes

1. A complete list of all structures indexed and notes is available in the files:

 * UALIB_Chemical_Structures_REGID.ods (LibreOffice Calc)
 * UALIB_Chemical_Structures_REGID.csv (tab delimited)
 * UALIB_Chemical_Structures_REGID.sdf (SDfile)

2. **/StructureData/raw/CA_Marvin_19.27.0** - files in here are the the original ChemAxon 
MarvinSketch v19.27 .mrv, .smi, and .inchikey chemical structure files.

2. **/StructureData/raw/CSV** - files in here are the the original indexing files which
include ChemAxon MarvinSketch v19.27 Daylight SMILES, InChIKeys (v1.05 as computed by ChemAxon molconvert v19.27.0), our internal REGID, substance name, thesis citation, and permalink.

3. **/StructureData/rdkit_processed_csv** - same as number 2, only adding RDKit kekulized SMILES (RDKit 2019.09.2 release), calculated InChI and InChIKeys for the substances(InChIs v1.05 as computed by RDKit 2019.09.2 release). The RDKit version used is also labeled in the filename. Note that the PUBCHEM_EXT_DATASOURCE InChI and SMILES are from RDKit. 

4. **/StructureData/rdkit_processed_sdf** - SDfile containing RDKit connection table, and 
the following SDfile data: SMILES (RDKit 2019.09.2 release), InChI (v1.05 as computed by RDKit 2019.09.2 release), our internal REGID, substance name,
thesis citation, and permalink. The RDKit version used is also labeled
in the filename. These files are submitted to PubChem.

## References

Much of our inspiration for this project came from the following similar project:

Andrews, D. M.; Broad, L. M.; Edwards, P. J.; Fox, D. N. A.; Gallagher, T.;
Garland, S. L.; Kidd, R.; Sweeney, J. B. The Creation and Characterisation of 
a National Compound Collection: The Royal Society of Chemistry Pilot. Chem. Sci. 2016,
7 (6), 3869–3878. [DOI:10.1039/C6SC00264A](https://doi.org/10.1039/C6SC00264A)

## Acknowledgments

Special thanks to the following current and past contributors... list them here [will update
tomorrow]

We are also grateful to ChemAxon for providing the MarvinSketch Academic Research License (thanks!). 

## Notes on Copyright and Reuse

Disclaimer: Not legal advice, just our own personal (non-lawyer) thoughtful 
interpretation.

The purpose of The University of Alabama Dissertation and Thesis indexing project 
is to allow greater discovery, use, and credit of the original authors' theses, 
not to claim any ownership of the written thesis content. The thesis authors hold the 
copyright to their own thesis.

We have only extracted and shared scientific facts (i.e., the chemical structures) and bibliographic
information from the theses. Such scientific facts and bibliographic data are not subject 
to U.S. copyright protection: 
[Compendium of U.S. Copyright Office Practices](https://www.copyright.gov/comp3/).
See specifically section 313.3(A), where examples are listed that are excluded 
from copyright protection, one of which mentions chemical structures:

..."DNA sequences and other genetic, biological, or chemical substances or 
compounds, regardless of whether they are man-made or produced by nature..."

In an effort to fully comply with copyright, Fair Use, and standard scholarly 
practice of reusing a thesis, we did not use any automated chemical structure 
extraction software. Instead, we drew our own chemical structures by using 
the theses as a reference and encoding the structures ourselves.

With that said, we are grateful to the thesis authors for their contributions
to science and have endeavored to credit their work respectfully and wherever 
possible by including a citation reference and permalink. The citation references and
permalinks are included on all shared chemical structure data including within
this Git Repository data files, The University of Alabama Institutional Repository,
and PubChem Substance Pages.

Our intention is for you to reuse the chemical structures 
however you like. All chemical structure data in this repository is licensed 
with [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please give the 
original authors of the theses credit by citing their work and following 
standard scholarly practice for reuse of the scientific literature, 
particularly if the chemical structure has led you to useful content within their 
thesis (as noted above, each thesis Author holds their own copyright). If you are
reusing a large corpus of the structures as a dataset, then it is appreciated 
if you cite our work as we put the effort into the indexing and data compilation. Lastly, any code in this repository is licensed under the BSD-2 license.

