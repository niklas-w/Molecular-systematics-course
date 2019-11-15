
# Bayesian inference with MrBayes

Bayesian inference differs from Maximum Likelihood in several ways and one of the main ones is that it takes into account prior probabilities. In the context of phylogenetic inference, this means that the parameter space can be constrained towards values (from parameters in the nucelotide subtitution model to fossil priors or biogeographic evidence) that are considered realistic based on the findings from previous studies. These in turn then influences the posterior probability of your hyphothesis, which in the case of phylogenetic inference is the phylogeny with its topology, branch lengths, and all of the sequence evolution model parameters.

Fot this practical, we will work with MrBayes. MrBayes is a program that incorporates model choice across a wide range of phylogenetic and evolutionary models. MrBayes uses Markov chain Monte Carlo (MCMC) methods to estimate the posterior distribution of model parameters. MrBayes may be downloaded as a pre-compiled executable or in source form from [here](http://nbisweden.github.io/MrBayes/download.html). For more detailed instructions click [here](https://github.com/NBISweden/MrBayes/blob/develop/INSTALL)

This is a ”user unfriendly” program, i.e. it is command driven and opens up in the terminal window. To use it, you need to know the sequence of commands that need to be input into the program. 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/MrBayes1.png" alt="MrBayes1" width="600"></p>

The first thing is to prepare your dataset (which is in the NEXUS format). MrBayes analyses can be done either by command line step by step or by adding all the parameters and different data partitions to your data file. You can add this information in a text editor at the end of your data file. See the following example: 


<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/MrBayes_example.png" alt="MrBayes_example" width="600"></p>

Open your text editor and simply add at the end of your `DatasetMB.nex` file this block:

```
begin mrbayes;

	charset Subset1 = 1-1450\3;
	charset Subset2 = 2-1450\3;
	charset Subset3 = 3-1450\3;
	charset Subset4 = 1451-2690\3 2693-3113\3;
	charset Subset5 = 2691-3113\3 2692-3113\3 1452-2690\3;
	charset Subset6 = 1453-2690\3;

	partition PartitionFinder = 6:Subset1, Subset2, Subset3, Subset4, Subset5, Subset6;
	set partition=PartitionFinder;
    
    set autoclose=yes;

	lset applyto=(1) nst=6 rates=invgamma;
	lset applyto=(2) nst=2 rates=propinv;
	lset applyto=(3) nst=2 rates=gamma;
	lset applyto=(4) nst=6 rates=gamma;
	lset applyto=(5) nst=6 rates=invgamma;
	lset applyto=(6) nst=1;

    prset applyto=(all) ratepr=variable brlensp=unconstrained:Exp(100.0) shapepr=exp(1.0) tratiopr=beta(2.0,1.0);
    unlink statefreq=(all) revmat=(all) shape=(all) pinvar=(all) tratio=(all);

    mcmc ngen=2000000 printfreq=1000 samplefreq=1000 nchains=4 nruns=2 savebrlens=yes [temp=0.11];
    sump relburnin=yes [no] burninfrac=0.25 [2500];
    sumt relburnin=yes [no] burninfrac=0.25 [2500] contype=halfcompat [allcompat];
END;
```

After you prepare the NEXUS file, save it as `DatasetMBrun.nex`. Next, open a terminal, run MrBayes and finally run your analysis by writing ”Execute" filename (provide the path of your file). 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/MrBayes3.png" alt="MrBayes3" width="600"></p>

If the dataset is okay, the analysis should look like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/MrBayes4.png" alt="MrBayes4" width="600"></p>

As we mentioned before, another way to run the program is by giving the commands step by step. You only need your dataset and partition in the NEXUS format. To do so, follow these instructions: 

Write ”Execute filename” (obviously replacing ”filename” with the name of your data file). This assumes that the input file is in the same directory as the MrBayes executable. If you have different data partitions (e.g. different genes) in the data file, take care to define these character sets using the charset command. 

The next thing to do is to define the model you want to use to analyze your dataset: ”lset nst=6 rates=invgamma” gives you the GTR+I+G model (see the manual for the other kinds of models). 

Now it is time to run your first analysis. This is done with the command ”mcmc” with a string of options after it, eg ”mcmc ngen=10000 printfreq=100 samplefreq=100 savebrlens=yes;”. This will run 10000 generations, sampling trees and parameters every 100 generations and printing to the screen every 100 generations (so that you can follow what is happening). Branch lengths of the trees are also saved (which makes bigger files). When 10000 generations have been done, the program will ask whether it should continue (unless you specify ”set autoclose=yes;” in the beginning, in which case the analysis terminates). Write in ”no” for the time being.

Once the analysis is done, you will notice several new files have appeared in your folder where the program and your dataset are. These include filename.mcmc, filename.run1.p, filename.run1.t, filename.run2.p and filename.run2.t. the *.p files contain the sampled parameter values and log likelihoods, the *.t files contain all sampled trees. 
	
Now you have to determine the burn-in, which means how many sampled generations from the beginning you need to discard. This can be done by giving the command ”sump”. ”sump” summarizes the parameter valuess in both the *.p files, but importantly for now, it generates a graph showing the development of the log likelihood values over the sampled generations. Scroll upwards in the Command box if you do not see the graph. You can visually inspect the graph to see where equilibrium is reached and you can discard all generations before that. To double check, you can run the command again, this time with the number of sampled generations to be discarded, e.g. ”sump burnin=20”. If the graph looks fine, then it is time to summarize the trees with the command ”sumt burnin=20”. This generates 3 new files filename.con, filename.parts and filename.trprobs. For the time being the first file is the most important, it includes the 50%-majority rule tree for the dataset including branch lengths and posterior probabilities. Add the extension .tre to this file and open it in FigTree and click on the ”Phylogram” button to view the branch lengths, and the ”Internal labels” button to view the posterior probabilities.
	

