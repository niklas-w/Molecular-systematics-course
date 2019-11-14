# **Model Selection**


In the other two tutorials you have learned to download various gene sequences from Genbank and align and concatenate them to create the dataset we want to work on for the rest of the workshop. You also heard about differences between different file formats and saw how to create the needed formats. For the next tutorial, we are going to use *PartitionFinder* to find the best partitioning scheme for our dataset and also the best models for each partition.

First remember that our final dataset, `COI_EF1a_Wingless.fasta` was saved as a fasta format (If you did not manage to generate this file, go to *Molecular-systematics-course/Data/* and download `2_COI_EF1a_Wingless.fasta`). Now open *Aliview* and open this file. You should have something similar to this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/3.ModelSelection/Aliview3.png" alt="Aliview3" width="800"></p>

Now I want you to save a \*.phy and a \.nex alignment file with the name **Dataset**. Use the options "*Save as Nexus*" and "*Save as Phylip (full names & padded)*" as seen in the next picture (both options marked with a red rectangle):

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/3.ModelSelection/Aliview5.png" alt="Aliview5" width="800"></p>

You should have the next files now:

```
Dataset.phy
Dataset.nex
```

For this tutorial we are going to use the `Dataset.phy` and a control file that we are going to create together. The control file has different blocks that you need to modify based on your analysis. On your text editor create a new file and save it as `partition_finder.cfg`. Copy/Paste inside the file the next block:

```
## ALIGNMENT FILE ##
alignment = infile.phy;

## BRANCHLENGTHS: linked | unlinked ##
branchlengths = unlinked;

## MODELS OF EVOLUTION: all | allx | mrbayes | beast | gamma | gammai | <list> ##
models = mrbayes;

# MODEL SELECCTION: AIC | AICc | BIC #
model_selection = BIC;

## DATA BLOCKS: see manual for how to define ##
[data_blocks]

**REPLACE ME BY YOUR PARTITIONS INFORMATION!**

## SCHEMES, search: all | user | greedy | rcluster | rclusterf | kmeans ##
[schemes]
search = greedy;

```

For *ALIGNMENT FILE* section you have to provide the name of the alignment file which is in this case `Dataset.phy`. But in this case as we are going to run the job on an online platform, the platform ask us to use `alignment = infile.phy;`. In the *DATA BLOCKS* you have to use the partition information we created yesterday and saved as `partitionsCodon.txt`. Take a look at the other options, what else you can modify?

We are going to use an online platform to run *PartitionFinder* as running it on your computer need spending some extra time for the installation step. The platform that we are going to use now is called *CIPRES*. It is a very useful online platform where you can run plenty of other programs also. But you need to register first, so click and open (in a new window) the following link: [www.phylo.org/portal2/login!input.action](https://www.phylo.org/portal2/login!input.action). You will see something like the next image. If you don’t have an account already, click or the red rectangle and register.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/3.ModelSelection/Cipres.png" alt="Cipres" width="800"></p>

When ypu log in you will see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/3.ModelSelection/Cipres2.png" alt="Cipres2" width="800"></p>

You have to click on *Create New Folder* and as *Label* you use `Course`. Now under you "Folders" you have a folder named *Course* and 2 other folders inside of it. Like the following picture:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/3.ModelSelection/Cipres3.png" alt="Cipres3" width="800"></p>

Click on *Data* subfolder then on *Upload/Enter Data*. Now you should be able to add the needed files by clicking on *Browse* and selecting the `Dataset.phy` and `partition_finder.cfg` files.
