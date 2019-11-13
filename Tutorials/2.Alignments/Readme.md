
# **MULTIPLE SEQUENCE ALIGNMENT**


From the first tutorial you have learned how to download data from Genbank, how to modify your fasta format sequence files and how to convert them to other sequence file formats. Just remember that the sequences are not aligned! It means that they have different lengths and nucleotide positions are not *homologous*! Here we are going to align our datasets using one of the most used aligners:


**MAFFT:** This is a multiple sequence alignment program for unix-like operating systems. We will be using an online version of the program at the following link: [https://mafft.cbrc.jp/alignment/server/](https://mafft.cbrc.jp/alignment/server/). But the installation of the program should be easy on all operating systems and optionally you can install it on your personal computer from [here](https://mafft.cbrc.jp/alignment/software/).

Open the link in a separate window. You should have something similar to this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT.png" alt="MAFFT" width="800"></p>

In the above picture, you see 2 red rectangles. the first one is where you click to upload your fasta format file and the second rectangle is where you can write your email to receive the aligned sequences. Remember to click on `Submit`! 

Here I uploaded the `COI2.fasta` file. You should see something similar to this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT2.png" alt="MAFFT2" width="800"></p>

Here again I have marked 2 red rectangles. In the one on the top of the page you can read `Fasta format`. We will click here in a few seconds, but before I wanted to show you something else. In the second red rectangle you can see the name of your sequences. Do you see something interesting in the format of the names? *They are all maximum 15 character long!* Also, you can see that the sequences are *interleaved*. The last line is a measure of how preserved a column is in your alignment.

Ok, let's click on Fasta format now. You will see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT3.png" alt="MAFFT3" width="600"></p>

Again *Voila*! You have your COI sequences aligned in the fasta format. Copy this and paste it in your text editor program. Save it as `COI_aligned.fasta`. 

Repeat this exercise for the other 2 genes. At the end you should have these 3 files:

```
COI_aligned.fasta
EF1a_aligned.fasta
Wingless_aligned.fasta
```

## Concatenation

Concatenation of sequences means adding sequences from the same organism but from different genes one after another in order to create a larger dataset for the analysis as opposed to analysing single-gene datasets. There are many programs available for concatenatenation of sequences. You can even concatenate your sequences with a text editor or using a few comands in any programming language if you feel confortable with it. Here we are going to use an online application.

[FaBox (1.5) - an online fasta sequence toolbox] (http://users-birc.au.dk/palle/php/fabox/index.php) is a useful online tool for simple tasks using fasta files. The webpage is developed by Aarhus University. Open the link on a new page. You should see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/Concat.png" alt="Concat" width="800"></p>

Please click on the only option which is red (*Fasta alignment joiner*). You should see this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/Concat2.png" alt="Concat2" width="800"></p>

Choose your `COI_aligned.fasta` file on the left and the `EF1a_aligned.fasta` file on the right. You should have something like this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/Concat3.png" alt="Concat3" width="800"></p>

Now click on *Save to disk* and save the `alignment.fasta` file on your computer. Rename this file to `COI_EF1a.fasta`. Remember that you can also just copy/paste the sequence directly from your browser and save them in your text editor. Now repeat the concatenation procedure and create the `COI_EF1a_Wingless.fasta` file.

Open Aliview and open the file you just created in it. You should see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/Aliview3.png" alt="Aliview3" width="800"></p>

So now we have the 3 genes concatenated in a single sequence alignment file. But what we don't see immediately in this "*Super Gene*" alignment is where each gene starts and ends in the alignment. One way to obtain this information is to open each gene's alignment `COI_aligned.fasta`, `EF1a_aligned.fasta` and `Wingless_aligned.fasta` in *Aliview* and look at their lengths. In our concatenated matrix we know the order of the genes...  so you can obtain the position of each gene easily. I want you to create a file in your text editor called `partitions.txt` and write down the information of each gene as:

```
COI = 1 - X;
EF1a = X+1 - Y;
Wingless = Y+1 - 3113;
```

where you find the correct value for `X` and `Y`. Now that you have the alignments open in *Aliview*, I want you to pay atention to the codon positions. Look at the following picture:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/Aliview4.png" alt="Aliview4" width="800"></p>

We want to write down the codon positions for each *partition* of our dataset. To find the correct reading frame and therefore the codon positions you can click on the button in the red rectangle on top left. Then you change the reading frame to find the one which has no stop codons in the alignment using the second red rectangle. *Do you know why?*  Also pay attention to the third red rectangle. In the picture we have the alignment of the *Wingless* gene. It is a protein coding nuclear gene, so the `Standard code` is the right option. But what about the *COI* gene?

To gain some time I will copy here how you should write down the codon positions for the partition file:

```
COI_pos1 = 1 - 1450\3;
COI_pos2 = 2 - 1450\3;
COI_pos3 = 3 - 1450\3;
EF1a_pos3 = 1451 - 2690\3;
EF1a_pos1 = 1452 - 2690\3;
EF1a_pos2 = 1453 - 2690\3;
Wingless_pos1 = 2691 - 3113\3;
Wingless_pos2 = 2692 - 3113\3;
Wingless_pos3 = 2693 - 3113\3;
```

Copy/Paste this in your text editor and save it as `partitionsCodons.txt`. Now we are ready to find out which partitioning scheme is best for our dataset in the next tutorial.


