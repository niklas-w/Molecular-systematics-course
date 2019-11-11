
# **MULTIPLE SEQUENCE ALIGNMENT**


From the first tutorial you have learned how to download data from Genbank, how to modify your fasta format sequence files and how to convert it to other sequence file formats. Just remember that the sequences are not aligned! It means that they have different lengths and nucleotide positions are not *homologous*! Here we are going to align our datasets using one of the most used aligners:


**MAFFT:** This is a multiple sequence alignment program for unix-like operating systems. We will be using an online version of the program at the following link: [https://mafft.cbrc.jp/alignment/server/](https://mafft.cbrc.jp/alignment/server/). But the installation of the program should be easy on all operating systems and optionally you can install it on your personal computer from [here](https://mafft.cbrc.jp/alignment/software/).

Open the link in a separate window. You should have something similar to this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT.png" alt="MAFFT" width="800"></p>

In the above picture, you see 2 red rectangles. the first one is where you click to upload your fasta format file and the second rectangle is where you can write your email to receive the aligned sequences. Remember to click on `Submit`! 

Here I uploaded the `COI2.fasta` file. You should see something similar to this now:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT2.png" alt="MAFFT2" width="800"></p>

Here again I have marked 2 red rectangles. On the one on the top of the page you can read `Fasta format`. We will click here in few seconds, but before I wanted to show you something else. in the second red rectangle you can see the name of your sequences. What is interesting in the format of the names? *They are all maximum 15 character long!* Also if you pay attention the sequences are *interleaved*. The last line is also a measure of how preserved a column is in your alignment.

Ok, let click on Fasta format now. you will see probably something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/2.Alignments/MAFFT3.png" alt="MAFFT3" width="600"></p>

Again *Voila*! You have your COI sequences aligned in fasta format. Copy it and paste it in your text editor program. Save it as `COI_aligned.fasta`. 

Repeat this exercise for the other 2 genes also. At the end you should have these 3 files:

```
COI_aligned.fasta
EF1a_aligned.fasta
Wingless_aligned.fasta
```

## ** Concatenation **

