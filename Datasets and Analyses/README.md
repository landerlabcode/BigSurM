# Datasets
This folder contains the datasets and scripts used for the analyses found in ["Leveraging gene correlations in single cell transcriptomic data"][1].

## Contents
- rajDropSeq4.mx: a Mathematica object file containing the "matpac" which holds the primary dataset used in analyses. This is a dataset from droplet-based sequencing of a subcloned WM989 melanoma cells ([GEO Accession GSE99330][2]) which has been preprocessed to remove all pseudogenes (comprehensive lists of human pseudogenes were obtained from [HGNC and BioMART][3]) and any genes which were expressed in fewer than eight cells.

- clusterIDs_1_2_3.mx: a Mathematica object file containing a list with associations between clusters 1, 2, and 3 and their respective cells.

- clusterIDs_1.1_1.2.mx: a Mathematica object file containing a list with associations between clusters 1.1 and 1.2 and their respective cells.

- Code_for_Figures.nb: a Mathematica notebook file which contains all relevant code and documentation to recreate figures found in [the paper][1].

- for Figure 2: a folder containing both Mathematica files and .mtx files containing the synthetic datasets necessary to recreate the figures found in Figure 2.

- ppiPairsAll.csv: a compiled list of 790,008 interacting protein-protein pairs compiled from the STRING and [HIPPIE][4] databases. STRING was queried using [BioMART][3] Of these, we used only those 523,292 pairs involving genes both of which were present in the matpac being analyzed (for trivial reasons, a gene pair  involving  a gene not in the matpac could never be found among correlated gene pairs derived from that matpac).

- paralogs.csv: a file containing the 3,132 pairs of human paralogs identified in [Hu et al, 2022][5]. Of these, 1,425 contained only genes that were both present in the matpacs analyzed.  

- significantCommunities.mx: a Mathematica object file containing the significant communities identified by BigSur from cluster 1.2.

[1]: https://www.biorxiv.org/content/10.1101/2023.03.14.532643v1 "Leveraging gene correlations in single cell transcriptomic data"

[2]: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE99330 "Torre et al, 2019"

[3]: https://biomart.genenames.org/ "HGNC Biomart Server"

[4]: http://cbdm-01.zdv.uni-mainz.de/~mschaefer/hippie/ "Human Integrated Protein-Protein Interaction rEference"

[5]: https://doi.org/10.1016/j.csbj.2022.11.041 "Hu et al, 2022"