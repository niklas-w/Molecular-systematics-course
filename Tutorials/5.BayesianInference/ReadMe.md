
# Bayesian inference with MrBayes

Bayesian inference differs from Maximum Likelihood becase take into account prior probabilities. In the context of phylogenetic inference, this means that parameters could be constrained towards values (from fossils or biogeographic evidence) that are considered realistic based on the findings of previous studies on the group of interest. These in turn can then inform the timing in other parts of the phylogeny so that an overall timeline of diversification can be estimated.

Fot this practical, we will work with MrBayes. MrBayes is a program for Bayesian inference and model choice across a wide range of phylogenetic and evolutionary models. MrBayes uses Markov chain Monte Carlo (MCMC) methods to estimate the posterior distribution of model parameters. MrBayes may be downloaded as a pre-compiled executable or in source form from [here](http://nbisweden.github.io/MrBayes/download.html). For more detailed instructions click [here](https://github.com/NBISweden/MrBayes/blob/develop/INSTALL)

This is a ”user unfriendly” program, ie it is command driven and opens up in the terminal window. To use it, you need to know the sequence of commands that are input into the program. 

https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/5.BayesianInference/MrBayes1.png

The first thing to do is open your dataset (which is in NEXUS format) in the program. To do so, write ”Execute filename” (obviously replacing ”filename” with the name of your data file). This assumes that the input file is in the same directory as the MrBayes executable. If you have different data partitions (eg different genes) in the data file, take care to define these character sets using the charset command. 

The next thing to do is define the model you want to use to analyze your dataset: ”lset nst=6 rates=invgamma” gives you the GTR+I+G model (see the manual for the other kinds of models). Now it is time to run your first analysis. This is done with the command ”mcmc” with a string of options after it, eg ”mcmc ngen=10000 printfreq=100 samplefreq=100 savebrlens=yes;”. This will run 10000 generations, sampling trees and parameters every 100 generations and printing to the screen every 100 generations (so that you can follow what is happening). Branch lengths of the trees are also saved (which makes bigger files). When 10000 generations have been iterated, the program will ask whether it should continue (unless you specify ”set autoclose=yes;” in the beginning, in which case the analysis terminates). Write in ”no” for the time being.

	Once the analysis is done, you will notice several new files have appeared in your folder where the program and your dataset are. These include filename.mcmc, filename.run1.p, filename.run1.t, filename.run2.p and filename.run2.t. the *.p files contain the sampled parameter values and log likelihoods, the *.t files contain all sampled trees. 
	
	Now you have to determine what the burn-in is, how many sampled generations from the beginning do you have to discard? This can be done by giving the command ”sump”. ”sump” summarizes the parameter valuess in both the *.p files, but importantly for now, it generates a graph showing the development of the log likelihood values over the sampled generations. Scroll upwards in the Command box if you do not see the graph. You can visually inspect the graph to see where equilibrium is reached and you can discard all generations before that. To double check, you can run the command again, this time with the number of sampled generations to be discarded, eg ”sump burnin=20”. If the graph looks fine, then it is time to summarize the trees with the command ”sumt burnin=20”. This generates 3 new files filename.con, filename.parts and filename.trprobs. For the time being the first file is the most important, it includes the 50%-majority rule tree for the dataset including branch lengths and posterior probabilities. Add the extension .tre to this file and open it in FigTree and click on the ”Phylogram” button to view the branch lengths, and the ”Internal labels” button to view the posterior probabilities.
	
	It is also possible to automate the described analysis entirely by placing the following lines of text at the end of your data file:

begin mrbayes;
	set autoclose=yes;
	lset nst=6 rates=invgamma;
	mcmc ngen=100000 printfreq=1000 samplefreq=1000 savebrlens=yes;
      sumt burnin=20;
end;