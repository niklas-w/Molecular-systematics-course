# Maximum-Likelihood Phylogenetic Inference


**Part I**: In this tutorial, we wiil analyse the butterfly dataset with with one of the fastest maximum-likelihood based phylogenetic program [IQ-TREE](http://www.iqtree.org) ([Nguyen et al. 2015](https://academic.oup.com/mbe/article/32/1/268/2925592)). IQ-TREE for Windows, MacOSX and Linux can be downloaded [here](http://www.iqtree.org/#download), you can install it on your personal computer (optional).

The quickest is to try out the IQ-TREE web server, where you only need to upload an alignment, choose the options and start the analysis.

**Tree inference**
Tree Inference provides the most frequently used features of IQ-TREE and allows users to carry out phylogenetic analysis on a multiple sequence alignment (MSA). In the most basic case, no more than an MSA file is required to submit the job. Without further input, IQ-TREE will run with the default parameters and auto-detect the sequence type as well as the best-fitting substitution model. Additionally, Ultrafast Bootstrap (Hoang et al., 2018) and the SH-aLRT branch test (Guindon et al., 2010) will be performed.
You can either try out the web server with an example alignment by ticking the corresponding box or upload your own alignment file. By clicking on ‘Browse’ a dialog will open where you can select your MSA; the file formats Phylip, Fasta, Nexus, Clustal and MSF are supported.

<p align="center"><img src="http://www.iqtree.org/doc/images/tut1.png" alt="IQTREE" width="600"></p>

After that you can submit the job. If you provide an email address, a notification will be sent to you once the job is finished. In case you don’t specify an email address, you will receive a link in the next step; you can bookmark this link to retrieve your results after the job is finished.

**Model Selection**
IQ-TREE supports a wide range of substitution models for DNA, protein, codon, binary and morphological alignments. In case you do not know which model is appropriate for your data, IQ-TREE can automatically determine the best-fit model for your alignment. Use the Model Selection tab if you only want to find the best-fit model without doing tree reconstruction.

<p align="center"><img src="http://www.iqtree.org/doc/images/tut2.png" alt="IQTREE" width="600"></p>

Like with Tree Inference, the only obligatory input is a multiple sequence alignment. You can either upload your own alignment file or use the example alignment to try out the web server and then submit the job.
