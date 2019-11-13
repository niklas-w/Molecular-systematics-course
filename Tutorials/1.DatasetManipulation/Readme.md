# **Dataset Manipulation**

## **Introduction**

In this section we will learn to download genetic sequence information from online databases (i.e. Genbank) and generate a dataset. Later on, by following tutorials, you will align this dataset file and convert it to different alignment file formats. We will also learn here how to convert between different formats used in phylogenetic programs and the main differences between these formats.

## **Download the data**

Using a web browser, you need to navigate to the NCBI’s Genbank. Even if the [link]( https://www.ncbi.nlm.nih.gov/genbank/) is not easy to remember, googling basically any keyword combination containing Genbank will bring you to the NCBI quite easily. In Genbank each sequence entry has a unique identification code called ***accession number***. For this exercise, you need to download the sequences of the following accession numbers.

| # | Code | Organism name | COI Acc. N. | EF1a Acc. N. | Wingless Acc. N. |
|---|---|---|---|---|---|
| 1 | CP07-44 | Marpesia zerynthia | KM012966 | KM013048 | KM013115 |
| 2 | NW89-13 | Hypanartia dione | HQ734933 | HQ734953 | HQ734843 |
| 3 | NW68-11 | Colobura dirce | AY090228 | AY090196 | AY090162 |
| 4 | NW39-2 | Araschnia levana | AY248780 | AY248805 | AF412762 |
| 5 | NW82-15 | Asterocampa leilia | KM012928 | AY218257 | AY218275 |
| 6 | NW63-3 | Aglais urticae | AY248786 | AY248811 | AF412777 |
| 7 | NW68-5 | Anartia amathea | AY788606 | AY788708 | AY788469 |
| 8 | NW76-2 | Eresia eranites | AY788617 | AY788722 | AY788483 |
| 9 | NW73-14 | Melitaea cinxia | AY788656 | AY788776 | AY788536 |
| 10 | NW85-13 | Junonia coenia | AY788643 | AY248801 | AY248826 |
| 11 | NW11-4 | Phyciodes cocyta | AF187755 | AY090192 | AY090158 |
| 12 | NW81-5 | Rhinopalpa polynice | AY788674 | AY788812 | AY788572 |
| 13 | NW63-21 | Vanessa atalanta | AY090221 | AY090187 | AF412772 |
| 14 | NW96-5 | Vanessula milca | AY788691 | AY788829 | AY788589 |
| 15 | NW62-1 | Chlosyne janais | AY788620 | AY788730 | AY788491 |
| 16 | NW87-3 | Tigridia acesta | AY788684 | AY788822 | AY788582 |
| 17 | NW130-15 | Baeotus beotus | AY788615 | AY788720 | AY788481 |

Pictures of the actual voucher specimens used to generate the sequences above.
<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Butterflies_for_tutorial.png" alt="Butterflies" width="800"></p>




Opening the [link]( https://www.ncbi.nlm.nih.gov/genbank/) provided earlier you can see the following (slight differences may exist due to different web browsers and operating systems and the position of the planets and …).


<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank1.png" alt="Genbank1" width="800"></p>


In the red rectangle you see a list option which should be on ***Nucleotide***. Clicking on the list you can see other repositories offered by NCBI website. Here we are going to create a dataset of nucleotide sequences of three protein coding genes, so we chose the ***Nucleotide*** option. Remember that these two markers being protein coding genes, allow us to create also ***Amino Acid*** datasets. *Do you know why we stay with nucleotides in this case? Wich option allows you to create an amino acid dataset?*

Now pick an accession number from the list and hit search. You should see something similar to this picture:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank2.png" alt="Genbank2" width="800"></p>

Take a look at it. Try to decipher different parts of it. Now look at the 2 red rectangles on top of the picture. The one on the left where you can read ***GenBank*** is the format of the information. And the other rectangle ***Send to:*** create a downloadable file. Click on it. Choose ***Complete Record***, ***File*** under *Choose Destination* and finally in *format:* choose ***FASTA***. 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank3.png" alt="Genbank3" width="800"></p>

Now ***Create File***! And *Voila!* Congratulations, now you have downloaded your first Fasta file.

Now download all sequences for each gene separately. ***IMPORTANT TIP*** Do not download each accession number separately! Go to this link ([www.ncbi.nlm.nih.gov/sites/batchentrez](https://www.ncbi.nlm.nih.gov/sites/batchentrez)) and follow the instructions for a batch download ;) Also remember to change the name of your files to the name of their genes. Now you should have these 3 files:

```
COI.fasta
EF1a.fasta
Wingless.fasta
```

---------

Now lets take a look at the *FASTA* files we have created. Open any of them in your (prefered) text editor. (Here I have used TextWrangler!)

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/FastaFile.png" alt="FastaFile" width="800"></p>

As you can see, each entry is something similar to this:

```
>AF412762.1 Araschnia levana voucher NW39-2 wingless (wg) gene, partial cds
TCCTGCACCGTTAAAACTTGTTGGATGAGGCTGCCCAGTTTTCGCTCCGTAGGTGATGCGCTAAAAGATC
GCTTCGATGGAGCGTCGCGGGTCATGATGCCCAATACTGAAATCGAAGCACCCGCACAGCGAAATGACGC
ATCGCCTCATCGAGTTCCAAGACGAGATCGGTACAGATTCCAGCTTCGACCGCACAATCCCGATCATAAA
ACACCGATTGCAAAAGACCTAGTCTACCTTGAATCATCACCAGGTTTTTGTGAGAAAAACCCGAGGCTGG
GCATTCCCGGCACACACAACGATACGAGCATCGGCGTCGACGGTTGCGATCTTATGTGTTGTGGTCGTGG
TTACCGTACTGAAACAATGCTTGTTGTGG

```

The line starting with `>` in a fasta file is a header for the sequence. Practically all programs will have problems with how Genbank have created these fasta files. So in your text editor go and modify the name of each sequence to keep only the organism name. Remember that an empty space is not allowed in the name! Replace it with an underscore `_`. You should have exactly the same header as bellow now.


```
>Araschnia_levana
TCCTGCACCGTTAAAACTTGTTGGATGAGGCTGCCCAGTTTTCGCTCCGTAGGTGATGCGCTAAAAGATC
GCTTCGATGGAGCGTCGCGGGTCATGATGCCCAATACTGAAATCGAAGCACCCGCACAGCGAAATGACGC
ATCGCCTCATCGAGTTCCAAGACGAGATCGGTACAGATTCCAGCTTCGACCGCACAATCCCGATCATAAA
ACACCGATTGCAAAAGACCTAGTCTACCTTGAATCATCACCAGGTTTTTGTGAGAAAAACCCGAGGCTGG
GCATTCCCGGCACACACAACGATACGAGCATCGGCGTCGACGGTTGCGATCTTATGTGTTGTGGTCGTGG
TTACCGTACTGAAACAATGCTTGTTGTGG

```

Now save the files adding `2` after the name of the genes. You should have the following files now:


```
COI2.fasta
EF1a2.fasta
Wingless2.fasta
```

Now we can proceed to the next tutorial to learn about Alignment Methods. But before lets take a look at our sequence files in a graphical interface specifically designed to visualize sequences and alignments, ***Aliview***.

Open the program, click on file, Open File and find any of the last fasta files you have created, for example `Wingless2.fasta`. You should see something like this.

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Aliview.png" alt="Aliview" width="800"></p>

Before moving on, consider what this file looks like. Very few sites look  ***aligned***, right? This a quite small dataset of relatively conserved sequences, so you can easily find patterns within the file and you should be able to align it by hand given enough time with no major problems. We will check our alignment once we obtain it in this program again.

Now if you click again on `File` you will see something like this:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Aliview2.png" alt="Aliview2" width="500"></p>

As you can see this program allow us to convert/save a sequence file in many different formats which can be used in different programs. Remember this for when we are going to convert the alignment to other file formats than fasta.

