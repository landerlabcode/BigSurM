# BigSurM (BigSur Mathematica)

BigSurM is a Mathematica tool for single cell RNA sequencing analysis which interfaces with "matpac" objects to
- Select statistically significant features to use in clustering.
- Identify statistically significant correlations between genes.

The principles surrounding these analyses are described in ["Leveraging gene correlations in single cell transcriptomic data"][1].

## Installation
BigSurM can be installed to the desired directory by cloning the repository.

```console
git clone https://github.com/landerlabcode/BigSurM
```
## Usage
BigSurM operates on "matpac" objects. Matpac objects are lists which contain four components: the sparse matrix of raw counts from the scRNAseq (genes x cells), the names of the genes, the cell ID's, and various metadata (in that order). An example of a matpac object can be found in the **Datasets** subdirectory (rajDropSeq4.mx). 

Once a matpac object is created, open the BigSur.nb file found in the main directory and Evaluate Notebook. This will load in all of the necessary functions for BigSurM to run.

BigSur can now be run in the notebook of your choosing using the following:
```
BigSur[matpac, c, filemarker, depthscaling, Options]
```
The parameters here are:
- matpac: The matpac containing **at least** the sparse matrix of raw counts and the names of the genes. **Ensure the sparse matrix does not contain any genes with zero counts in any cell.** In addition, one should make sure that the list of gene names and list of cell IDs do not contain any duplicates.  
- c: The coefficient of variation that you wish to use in your analysis. The function **FindBestCAlt** can be used to determine a best-fit value for the coefficient of variation. See documentation within the notebook for more details.
- filemarker: Text indicating the beginning of the names of files that will be generated and saved. 
- depthscaling: If you supply a list, that list of values will be used to determine how to scale the counts to determine the cell-specific means of each gene. Otherwise, pass Auto to have these calculated for you. See documentation on **FindBestCAlt** for more details.

The options that can be passed are:
- "Correlations":   Default = False.  When set to False, only the Fano factors and their statistics are calculated.  When set to True both Fano factors and correlation coefficients are done.  
- "alpha"  Default: 0.02.  The FDR cutoff you wish to use
- "Pvalue"  Default: "BH".  "BH" means use the Benjamini Hochberg procedure to control the FDR.  Alternatively one may enter an arbitrary Pvalue cutoff.  If you enter any other text it will use a Bonferroni cutoff
- "First Pass Cutoff":  To avoid wasting time calculating p-values when one knows in advance they are going to be too large to matter, there is a default cutoff that gets passed to the function that finds the roots of the Cornish Fisher Polynomials, causing it to skip over cases where the roots can be judged quickly to correspond to such p-values.  The default is 2, meaning a pvalue of 10^-2.  
- "Fano Inverse Sqrt Moments"-> For each gene pair, the moments calculated to produce the Cornish Fisher Polynomials need to get corrected for the multiplication of the inverse of the geometric mean of the modified corrected  fano factors that occurs in generating PCC'.  That's a rather slow process, and the corrections tend to be very small for most genes.  Setting this option to False will suppress that step; some errors will be generated but the code will take less time to run.  Not a bad idea if one wants to just take a quick look see at how the results may come out.  
- "Find Communities"  The code can either end by returning an adjacency matrix, or it can continue on and use the Walktrap Algorithm to find gene communities, which is the default.  If you don't want it to do that last step, set this to False.  Finding communities by walktrap isn't usually particularly time consuming, but if the number of significant correlations is very large it can be.  A very large number of significant correlations is usually a sign of a great deal of cell heterogeneity, and in that situation one might not want to bother finding communities.

BigSurM will output a series of files, containing information like the modified corrected residual matrix, the modified corrected fano factors and their -log10 transformed pvalues, modified corrected PCCs, pvalues of significant gene gene correlations, and a gNO containing the equivalent PCC values of the significant correlations.  

To visualize the communities that arise from the calculated correlations, refer to documentation found in **"BigSur Visualization.nb"**

To utilize BigSur in clustering cells, refer to documentation found in **BigSur Subclustering.nb"**

[1]: https://www.biorxiv.org/content/10.1101/2023.03.14.532643v1 "Leveraging gene correlations in single cell transcriptomic data"