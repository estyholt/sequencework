# MCscan-utilities

Utility scripts for working with MCscan software, which is already installed and working in the Jupyter instances launchable [here](https://github.com/fomightez/mcscan-binder).

# The scripts

* get_if_chromosome_rearranged_func_AFTER_MCscan_simplified.py
> MCscan results --> assessment of whether significant rearrangement of the chromosome/genome has occured.

Developed primarily for core function `get_if_chromosome_rearranged("<anchors_file>")` to be used in Jupyter notebook environment. 
Needs to be run after performing the `python2 -m jcvi.compara.catalog ortholog` step. See the Example Workflow [here](https://github.com/tanghaibao/jcvi/wiki/MCscan-(Python-version)) for familiarizing yourself with that step.

There is a version that just reworks the code from the `dotplot.py` but that
was way longer than it needed to be because of the interconnectedness of the 
jcvi package parts, and so this oversimplifies what I assume
`get_if_chromosome_rearranged_func_based_on_mcscan.py` does. (There is no one-
to-one correspondance between the two implementations worked out.)

Note that this version only considers genes for which it has orthologs identified. This seems actually where this 'simplified' approach may be better than the one derived from the dotplot.py script, `get_if_chromosome_rearranged_func_based_on_mcscan.py`. That is because it looks like additional genes in one organism being compared cause the list of the query and subject genes to never match and always report a rearrangement.

Instead of requiring a sorted BED file among the input, i.e., so numerically 
gene position ascending, I use a simplified approach 
to determine order of genes/transcripts using coordinates in BED file.  
This simplified script will only work 
with a single chromosome (or single-chromosome genome). Again, use 
`get_if_chromosome_rearranged_func_based_on_mcscan.py` if you need overview
for multiple chromosomes.

Verified compatible with both Python 2.7 and Python 3.6.

Written to run from command line or pasted/loaded inside a Jupyter notebook cell.  
The main ways to run the script are demonstrated in [a notebook found here](https://github.com/fomightez/????). It can be run actively by pressing the `launch binder` button [there](https://github.com/fomightez/????). )



#### For running in a Jupyter notebook:

To use this script after pasting or loading into a cell in a Jupyter notebook, in the next cell define the URL and then call the main function similar to below:
```
get_if_chromosome_rearranged("S288c.N44.anchors") 
```
See [here](https://git.io/vh8M7) and for notebooks demonstrating use within a Jupyter notebook; click `launch binder` to launch the notebooks from there.


Related scripts by others
-------

Annotation by [MFannot](https://github.com/BFL-lab/Mfannot) is often part of using organelle genomic data. By default it produces a `masterfile` formatted outout file. That can be converted to a `GFF3` formatted annotation file, which is what MCscan needs to work with, via a Perl script called [mfannot2gff.pl](https://github.com/kbseah/mitonotate/blob/master/mfannot2gff.pl). That script is included in the [MITONOTATE Annotation pipeline for ciliate mitochondrial genomes](https://github.com/kbseah/mitonotate) created by Brandon Seah (kbseah@mpi-bremen.de).
