# **Dataset Manipulation**

## **Introduction**

In this section we will learn to download genetic sequence information from online databases (i.e. Genbank) and generate a dataset. Later on in following tutorials this dataset file will be aligned and converted to different alignment file formats. We will also learn here how to convert between different formats used in phylogenetic programs and the main differences between these formats.

## **Download the data**

You need to navigate using a web browser to the NCBI’s Genbank. Even if the [link]( https://www.ncbi.nlm.nih.gov/genbank/) is not easy to remember, googling basically any keyword combination containing Genbank will bring you to NCBI quite easily. In Genbank each sequence entry has a unique identification code called ***accession number***. For this exercise, you need to download the sequences of the following accession numbers.

| # | Organism name | COI Acc. N. | EF1a Acc. N. |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |
| 6 |  |  |  |
| 7 |  |  |  |
| 8 |  |  |  |
| 9 |  |  |  |
| 10 |  |  |  |
| 11 |  |  |  |
| 12 |  |  |  |
| 13 |  |  |  |
| 14 |  |  |  |
| 15 |  |  |  |

Opening the [link]( https://www.ncbi.nlm.nih.gov/genbank/) provided earlier you can see the following (slight differences may exist due to different web browsers and operating systems and the position of the planets and …).


<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank1.png" alt="Genbank1" width="600"></p>


In the red rectangle you see a list option which should be on ***Nucleotide***. Clicking on the list you can see other repositories offered by NCBI website. Here we are going to create a dataset of nucleotide sequences of two protein coding genes, so we chose the ***Nucleotide*** option. Remember that these two markers being protein coding genes, allow us to create also ***Amino Acid*** datasets. *Do you know why we stay with nucleotides in this case? Wich option allows you to create an amino acid dataset?*

Now pick an accession number from the list and hit search. You should see something similar to this picture:

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank2.png" alt="Genbank2" width="600"></p>

Take a look at it. Try to decipher different parts of it. Now look at the 2 red rectangles on top of the picture. The one on the left where you can read ***GenBank*** is the format of the information. And the other rectangle ***Send to:*** create a downloadable file. Click on it. Choose ***Complete Record***, ***File*** under *Choose Destination* and finally in *format:* choose ***FASTA***. 

<p align="center"><img src="https://github.com/niklas-w/Molecular-systematics-course/blob/master/Tutorials/1.DatasetManipulation/Genbank3.png" alt="Genbank3" width="600"></p>

Now ***Create File***! And *Voila!* Congratulations, now you have downloaded your first Fasta file.

Now download all sequences for each gene separately. ***IMPORTANT TIP*** Do not download each accession number separately! Go to this link ([www.ncbi.nlm.nih.gov/sites/batchentrez](https://www.ncbi.nlm.nih.gov/sites/batchentrez)) and follow the instructions for a batch download ;)

