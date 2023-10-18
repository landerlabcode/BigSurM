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
BigSurM operates on "matpac" objects. Matpac objects are lists which contain three components: the sparse matrix of raw counts from the scRNAseq, the names of the genes, and various metadata (in that order). An example of a matpac object can be found in the **Datasets** subdirectory (rajDropSeq4.mx). 

Once a matpac object is created, open the BigSur.nb file found in the main directory and Evaluate Notebook. This will load in all of the necessary functions for BigSurM to run.

BigSur can now be run in the notebook of your choosing using the following:
```
BigSur[matpac, c, filemarker, depthscaling, Options]
```
The parameters here are:
- matpac: The matpac containing **at least** the sparse matrix of raw counts and the names of the genes.
- c: The coefficient of variation that you wish to use in your analysis.
- filemarker: The title of the folder you wish to create when saving BigSur outputs.
- depthscaling: If you supply a list, that list of values will be used to determine how to scale the counts to determine the cell-specific means of each gene. Otherwise, pass False to have these calculated for you.

The options that can be passed are:
- Correlations: Boolean, default False. If true, BigSur will identify statistically significant gene-gene correlations.
- alpha: Float, default 0.02. Desired false discovery cutoff for labeling of statistically significant correlations.
- Pvalue: String, default "BH". Desired method for controlling false discoveries. The default will use Benjamini Hochberg.
- First Pass Cutoff: Integer, default 2. Removes roots before p-value calculations if the root is below Abs[Sqrt(2)\*InverseErfc(2*10^-first.pass.cutoff)]. The higher the number, the more correlations are removed in initial screening.
- Fano Inverse Sqrt Moments: Boolean, default True. If true, BigSur will calculate the moments for the inverse Fano factor pairs before performing Cornish Fisher expansion. Setting false will significantly speed up calculation at the cost of some accuracy.
- Interrupt: Boolean, default True. If true, Mathematica will show you how well the estimated value of the coefficient of variation fits to your data. If it is poorly fit, you can try another value.
- Find Communities: Boolean, default True. If true, BigSur will find communities within the total adjacency matrix using the walk trap algorithm and return a list containing each community.

[1]: https://www.biorxiv.org/content/10.1101/2023.03.14.532643v1 "Leveraging gene correlations in single cell transcriptomic data"