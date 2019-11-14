

# Divergence Time Inference with BEAST2

In previous days we saw how to prepare molecular datasets, how to find the best partitioning scheme and best substitution model; and we finally saw how to infer phylogenies using **Bayesian** and **Maximum Likelihood** approaches. We very briefly saw how to interpret the obtained trees and how to check the obtained results.

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

Copy/Paste it at the end of your nexus file and save it as `DatasetBEAST.nex`. Now we want to create **BEAST**'s command file which is a `*.xml` file. This is done using the program **BEAUti**.

Open **BEAUti** from the BEAST2 folder, and import the alignment. To do so, click on **"File"** and click on **"Import Alignment"**. Find your alignment file called `DatasetBEAST.nex` and import it. The BEAUti window should then look as shown in the screenshot below.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast1.png" alt="Beast1" width="800"></p>

The BEAUti interface has six different tabs, of which (at the top of the window), the first one "Partitions" is currently selected. First need to specify settings regarding the partitioning in the currently open tab. 

Select the 3 partitions rows and click on **Link Trees** and **Link Clock Models** near the top of the BEAUti window. This will force BEAST2 to use all partitions together to infer a tree or a clock model. Also rename **Clock Model** name of the partitions to `clock` by changing the **Clock Name** for any of the partitions and hitting enter! Do the same for the **Tree** and call it `tree`. Now you should have something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast2.png" alt="Beast2" width="800"></p>

The settings in the **Partitions** tab are now complete. Now remember the result from *PartitionFinder* for each partition. These are the "Substitution Models" we want to set. I will copy it again here:

```
Subset | Best Model | # sites    | subset id                        | Partition names
1      | GTR+I+G    | 2075       | d1a04f8fd764b835133798f90a299406 | EF1a_pos2, COI_pos2, COI_pos1, EF1a_pos1, Wingless_pos1, Wingless_pos2                              
2      | HKY+G      | 483        | a025b1f5af55bcc97f43596191b3173e | COI_pos3
3      | GTR+G      | 555        | 9962ca78e0bdee4c13544ee243422b2d | EF1a_pos3, Wingless_pos3
```

Click on the **Site Model** tab next. In this tab we can specify the substitution models for all our partitions. This is a crucial step for our analysis to run well, so please pay extra attention.

Select the **Subset1** partition in the panel at the left. In front of the **Subst Model** click on the drop menu and choose `GTR`. To choose the `+G` option in our model, look for **Gamma Category Count** and write `4` in front of it in the empty space. Now to apply the `+I` option in the model, look for **Proportion Invariant** option, insert an initial value of `0.1` in the empty space and click in **estimate** box.

Now you should have something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast3.png" alt="Beast3" width="800"></p>

Do this carefully for the other Subsets also.

Next, click on the **Clock Model** tab. From the drop-down menu choose **Relaxed Clock Log Normal** model. This is the most commonly used relaxed clock model in which substitution rates of individual branches are drawn from a lognormal distribution. Now you should see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast4.png" alt="Beast4" width="800"></p>

Follow by clicking on the **Priors** tab. From the drop-down menu in front of the **Tree.t:tree** *prior*, select **Birth Death Model**. By doing so we add a parameter to the model for the extinction rate. If we would choose the alternative Yule model (Yule 1925), we would assume that no extinction has ever occurred. As this seems rather unrealistic, the birth-death model (Gernhard 2008) is in most cases the more appropriate choice. 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast5.png" alt="Beast5" width="800"></p>

Now on the bottom of the *priors* list you have the possibility of creating new ones by clicking on **Add Prior**. One of the important information that we want to include in a **Time Calibration Phylogeny** is the *Time* dimension. We will add this ***Prior*** using this button. The calibration points that we will be using for this exercise are extracted from Niklas' paper on the timing of butterflies. We will add time constraints on the age of the **most recent common ancestor** of a clade. The constraints that we will be using now are the ones in the next table:


| Constraint # | Clade | min Age | max Age |
|---|---|---|---|
| 1 | Araschnia, Aglais, Hypanartia and Vanessa | 34 My | 60 My |
| 2 | Melitaea, Chlosyne, Eresia and Phyciodes | 28 My | - |

Now click on **Add Prior**. A pop-up window should open asking **Which prior do you want to add**. Choose **MRCA prior**. and click `OK`. In **Taxon set label** write `Const1`for the first constraint. Add the 4 species from the table above by selecting them and hitting the arrows toward right empty space. You should have something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast6.png" alt="Beast6" width="800"></p>

Now hit **OK** and create the next constraint named `Const2`. Now you should have your two constraints. Force the monophyly on these clades by clicking on **monophyletic** box in front of their priors. Now for the first constraint, click on the drop-down menu in front of it and choose **Uniform** distribution. Then click on the triangle at the left of the **Const1.prior** to choose the ages. Here the **Lower** will be `34` and the **Upper** `60`. For the **Const2.prior** use a **Log Normal** distribution. In this distribution you have 2 parameters, **M** and **S**. **M** parameter is the mean and the **S** parameter define how asymmetrical is the distribution. As our min age for this clade is `28`, you can introduce this number in **Offset** and insert let say `40` for the **M** parameter. Now modifying the **S** value you can get a distribution which make sense for your constraint. Here we will use a value of `3.4` for **S** but play with this value a little until you get a feeling for how it affects the distribution. 

Now you should have this:


<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast7.png" alt="Beast7" width="800"></p>

Continue to the **MCMC** tab, where you can specify the run length. This analysis will require millions of **generation** before the MCMC chain reaches full stationarity (converges). For this exercise we recommend that you use a **Chain Length** of `200,000` states. Also modify the **Num Initialization Attempts** to `100`. Click on the triangle by **tracelog** and in **Log Every** modify the number to `200`. You should have something exactly like this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast8.png" alt="Beast8" width="800"></p>

Now close the **tracelog** by clicking on the triangle again and click on the triangles at the left of both **screenlog** and **treelog.t:tree** and modify the **Log Every** option to `200` also. You should now have this on the screen:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast9.png" alt="Beast9" width="800"></p>


Now click on **File** > **Save**, choose the folder you want, name your file `Dataset.xml` and click on **Save** again. Close **BEAUTi**. Now we will run the `Dataset.xml` file. Open **BEAST** and click on **Choose File**. You should be seeing this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Beast10.png" alt="Beast10" width="800"></p>

Click on **Run** button. It should be quite fast! When it is finished close the extra window, it will ask you if you want to save, respond **NO**.

## Analysing the results with Tracer

After the **BEAST** analysis is completed we will check the trace files in **Tracer**. Open **Tracer**. Drag and drop in the empty space at the left side of **Tracer**'s window, the log file created by BEAST named `DatasetBEAST.log`. You should see a trace somehow similar to this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Tracer.png" alt="Tracer" width="800"></p>

As you can see, clearly 200,000 generations are not enough! That is why I have run this analysis for 20,000,000 generations for you to check the trace file. Download it from [Data folder](https://github.com/niklas-w/Molecular-systematics-course/tree/master/Data). It is called `DatasetBEAST20M.log`. Open it in a new **Tracer** window. Is it enough or we have to run the analysis for longer? Check the trace for different parameters. Did all of them converged? is there any parameter which is still not well sampled?


## Obtaining the Time-tree

Now we will use the program **TreeAnnotator** from BEAST package. Open the program. In front of the **Burning Percentage** write `10`, In front of the **Input Tree File** choose the `tree.trees` file created by BEAST and in front of the **Output File** write `tree.trees.tre`. Click on the box in front of **Low Memory**. You should have this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/6.DivergenceTime/Tree.png" alt="Tree" width="800"></p>


Now hit **Run**. When the analysis is finished, open your final `tree.trees.tre` file in **FigTree**. Any surprises?

