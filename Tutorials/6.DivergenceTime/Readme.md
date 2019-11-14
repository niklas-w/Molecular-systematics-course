

# Divergence Time Inference with BEAST 2

In previous days we saw how to prepare molecular datasets, how to find the best partitioning scheme and best substitution model; and we finally saw how to infere phylogenies using **Bayesian** and **Maximum Likelihood** approaches. We very briefly saw how to interpret the obtained trees and how to check the obtained results.

In this tutorial, we will demonstrate how time-calibrated phylogenies can be inferred using a Bayesian approach. For this we will use the program BEAST2, which is a cross-platform program for Bayesian phylogenetic analysis of molecular sequences. BEAST 2 includes a graphical user-interface for setting up standard analyses and a suit of programs for analysing the results.

The data used in this tutorial is the concatenated alignment generated before `3_Dataset.nex`. Please download the data from [here](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/3_Dataset.nex). Again, the first step will be to delete the following lines added by *Aliview* in your text editor:

```
BEGIN ASSUMPTIONS;
EXSET * UNTITLED  = ;
END;

BEGIN CODONS;
CODONPOSSET * CodonPositions =
 N:,
 1: 1-3112\3,
 2: 2-3113\3,
 3: 3-3111\3;
CODESET  * UNTITLED = Universal: all ;
END;

BEGIN SETS;
END;
```
Now we are going to define the partitions as suggested by *PartitionFinder*. To do so, we will add a new data block at the end of our nexus file. The block is defined as follows:

```
begin sets;

 charset Subset1 = 1453-2690\3 2-1450\3 1-1450\3 1452-2690\3 2691-3113\3 2692-3113\3;
 charset Subset2 = 3-1450\3;
 charset Subset3 = 1451-2690\3 2693-3113\3;

end;

```

Copy/Paste it at the end of your nexus file and save it as `DatasetBEAST.nex`. Now we want to create **BEAST**'s comand file which is a `\*.xml` file. This is done using the program **BEAUti**.

Open **BEAUti** from the BEAST2 folder, and import the alignment. To do so, click on **"File"** and click on **"Import Alignment"**. Find your alignment file called `DatasetBEAST.nex` and import it. The BEAUti window should then look as shown in the screenshot below.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast1.png" alt="Beast1" width="800"></p>

The BEAUti interface has six different tabs, of which (at the top of the window), the first one "Partitions" is currently selected. First need to specify settings regarding the partitioning in the currently open tab. 

Select the 3 partitions rows and click on **Link Trees** and **Link Clock Models** near the top of the BEAUti window. This will force BEAST2 to use all partitions together to infere a tree or a clock model. Also rename **Clock Model** name of the partitions to `clock` by changing the **Clock Name** for any of the partitions and hitting enter! Do the same for the **Tree** and call it `tree`. Now you should have something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast2.png" alt="Beast2" width="800"></p>

The settings in the **Partitions** tab are now complete. Now remember the result from *PartitionFinder* for each partition. These are the "Substitution Models" we want to set. I will copy it again here:

```
Subset | Best Model | # sites    | subset id                        | Partition names
1      | GTR+I+G    | 2075       | d1a04f8fd764b835133798f90a299406 | EF1a_pos2, COI_pos2, COI_pos1, EF1a_pos1, Wingless_pos1, Wingless_pos2                              
2      | HKY+G      | 483        | a025b1f5af55bcc97f43596191b3173e | COI_pos3
3      | GTR+G      | 555        | 9962ca78e0bdee4c13544ee243422b2d | EF1a_pos3, Wingless_pos3
```

Click on the **Site Model** tab next. In this tab we can specify the substitution models for all our partitions. This is a crucial step for our analysis to run well, so please pay extra attention.

Select the **Subset1** partition in the panel at the left. In front of the **Subst Model** click on the drop menu and choose `GTR`. To choose the `+G` option in our model, look for **Gamma Category Count** and write `4` in front of it in the empty space. Now to apply the `+I` option in the model, look for **Proportion Invariant** option, insert an inicial value of `0.1` in the empty space and click in **estimate** box.

Now you should have something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast3.png" alt="Beast3" width="800"></p>

Do this carefully for the other Subsets also.

Next, click on the **Clock Model** tab. From the drop-down menu choose **Relaxed Clock Log Normal** model. This is the most commonly used relaxed clock model in which substitution rates of individual branches are drawn from a lognormal distribution. Now you should see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast4.png" alt="Beast4" width="800"></p>

Follow by clicking on the **Priors** tab. From the drop-down menu in front of the **Tree.t:tree** *prior*, select **Birth Death Model**. By doing so we add a parameter to the model for the extinction rate. If we would choose the alternative Yule model (Yule 1925), we would assume that no extinction have ever occurred. As this seems rather unrealistic, the birth-death model (Gernhard 2008) is in most cases the more appropriate choice. 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast5.png" alt="Beast5" width="800"></p>

Now on the bottom of the *priors* list you have the possibility of creating new ones by clicking on **Add Prior**. One of the important informations that we want to include in a **Time Calibration Phylogeny** is the *Time* dimension. We will add this ***Prior*** using this button. The calibration points that we will be using for this exercize are extracted from Niklas' paper on the timing of butterflies. We will add time constraints on the age of the **most common ancester** of a clade. The constraints that we will be using now are the ones in the next table:

| Clade | min Age | max Age |
|---|---|---|
| Araschnia, Aglais, Hypanartia and Vanessa | 34 My | 60 My |
| Melitaea, Chlosyne, Eresia and Phyciodes | 28 My | - |


Most of the other items shown in the "Prior" panel correspond to prior densities placed on the parameters of the substitution models for the partitions. You may keep the default priors for each of these parameters. However, to allow time calibration of the phylogeny, a prior density still needs to be specified for at least one divergence time, otherwise BEAST2 would have very little information to estimate branch lengths according to an absolute time scale. 

Continue to the "MCMC" tab, where you can specify the run length. This analysis will require a few hundred million iterations before the MCMC chain reaches full stationarity, which would take several days of run time. For this exercise we recommend that you use a chain length of 5,000,000 million states and either run the analysis or cancel the run after following it for some time, and then use output files from our analysis (you'll find the links below) for the rest of the tutorial. 

Also change the names of the output files: Click on the triangle to the left of "tracelog" and specify "Dataset.log" as the name of the log file. In the next field for "Log Every", set the number to "1,000" so that only every 1,000 MCMC state is written to the log file. Click on the triangle again, then click on the black triangle to the left of "treelog". Specify "Dataset.trees" as the name of the tree file and again use "1,000" as the number in the field for "Log Every". When the window looks as in the below screenshot, click on "Save" in BEAUti's "File" menu, and name the resulting file in XML format Dataset.xml. You can download [6.Dataset.xml](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/6.Dataset.xml) If you did not manage to complete this step.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast9.png" alt="Beast9" width="600"></p>

Now, open the program BEAST2 and select the file [6.Dataset.xml](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/6.Dataset.xml) as input file, as shown in the screenshot below. When you click the "Run" button, BEAST2 will start the analysis.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast10.png" alt="Beast10" width="600"></p>

# Analyzing the results with Tracer

After the two BEAST2 analyses have completed (or if you decided not to wait and use [the output](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/6.Dataset.log) of our analysis instead), open file [6.Dataset.log](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/6.Dataset.log) in the program Tracer. When the main window has opened, choose Import Trace File from the File menu and select the file that BEAST has created called Dataset.log.

Remember that MCMC is a stochastic algorithm so the actual numbers will not be exactly the same as those depicted in the figure. On the left hand side is a list of the different quantities that BEAST has logged to file. There are traces for the posterior (this is the natural logarithm of the product of the tree likelihood and the prior density), and the continuous parameters. Selecting a trace on the left brings up analyses for this trace on the right hand side depending on tab that is selected. When first opened, the ‘posterior’ trace is selected and various statistics of this trace are shown under the Estimates tab. In the top right of the window is a table of calculated statistics for the selected trace.

In the bottom left part of the Tracer window, you'll see statistics for the estimate of the posterior probability (just named "posterior"), the likelihood, and the prior probability (just named "prior"), as well as for the parameters estimated during the analysis (except the phylogeny, which also represents a set of parameters). The second column in this part shows the mean estimates for each parameter and their ESS values. Do the ESS values of all parameters indicate stationarity?

With the posterior probability still being selected in the list at the bottom left, click on the tab for "Trace" (at the very top right). You will see how the posterior probability changed over the course of the MCMC. This trace plot should ideally have the form of a "hairy caterpillar", but as you can see from the next screenshot, this is not the case for the posterior probability.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast11.png" alt="Beast11" width="600"></p>


<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast12.png" alt="Beast12" width="600"></p>

# Obtaining the tree

BEAST also produces a posterior sample of phylogenetic time-trees along with its sample of parameter estimates. These need to be summarized using the program TreeAnnotator. This will take the set of trees and find the best supported one. It will then annotate this representative summary tree with the mean ages of all the nodes and the corresponding 95% HPD ranges. It will also calculate the posterior clade probability for each node. Run the TreeAnnotator program and set it up as depicted in Figure 

The burnin is the number of trees to remove from the start of the sample. Unlike Tracer which specifies the number of steps as a burnin, in Tree Annotator you need to specify the actual number of trees. For this run, you specified a chain length of 5,000,000 steps sampling every 1,000 steps. Thus the trees file will contain 5,000 trees and so to specify a 10% burnin in the top text field.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast13.png" alt="Beast13" width="600"></p>

For the input file, select the trees file that BEAST created and select a file for the output (here we called it [6.Final.tree](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data/6.Final.tree)). Now press Run and wait for the program to finish.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast14.png" alt="Beast14" width="600"></p>

Finally, we can visualize the tree in FigTree. Run this program, and open the Final.tree file by using the Open command in the File menu. The tree should appear.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast15.png" alt="Beast15" width="600"></p>

To add a time scale to the phylogeny, set a tick next to "Scale Axis" in the menu on the left. Also click the triangle next to it, remove the tick next to "Show grid" in the newly opened menu field, but set a tick next to "Reverse axis" instead. The result is shown in the next screenshot.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast16.png" alt="Beast16" width="600"></p>

To also see the confidence intervals for the age estimates, click on the triangle next to "Node Bars" in the menu on the left. Also set a tick in the checkbox for "Node Bars". Choose the first item from the drop-down menu for "Display", the "height_95%_HPD" The phylogeny should then look as shown below.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/Beast17.png" alt="Beast17" width="600"></p>
Question

1. Is this topology consistent with that recovered from IQTREE and RAxML?


(This tutorial is modified from https://github.com/leimurillo/tutorials/tree/master/bayesian_phylogeny_inference).
