# Contents
- [Find data](#find-data)
- [Download data to the server](#download-data-to-the-server)

## Find data  
First, make sure you have done the instructions described in [00-Get_started.md](00-Get_started.md).  

As you have probably learned, there are many databases for HTS data. The two most common and comprehensive are probably [ENA - the European Nucleotide Archive](https://www.ebi.ac.uk/ena/browser/home) and the [NCBI SRA database](https://www.ncbi.nlm.nih.gov/sra).

We will use SRA today and download some public HTS data from SARS-CoV-2, the Covid-19 virus. There is a separate SARS-CoV-2 version of the SRA database, open its webpage by following [this link](https://www.ncbi.nlm.nih.gov/sars-cov-2/). Then, click on the link on the middle of the page with a number and "SRA runs" under it. You should now be on a page looking something like this (if not, click [here](https://www.ncbi.nlm.nih.gov/sra/?term=txid2697049%5BOrganism:noexp%5D%20NOT%200[Mbases)):  
<img src="/images/SRA.png" width="700" height="500">   

On the left side it's possible to filter the data. Click the following links:  
Library layout "paired"  
Platform "Illumina"  
Source "RNA" (SARS-CoV-2 is an RNA virus)  
File type "fastq"  
Strategy "other"  

Click on one of the results. 

Answer these questions:  
```diff
! What does "paired" library layout mean?
! How many sequence files can you expect from "paired" data?
! What is the "Run" accession for the sample you have selected? (begins with SRR... or ERR...).
````  

[Back to top](#contents)

## Download data to the server

We will use a SARS-CoV-2 dataset that is not too big so that our analysis does not take too much time. The run accession numbers for our data is SRR14253446.

At the top of the page, in the search bar, replace what is there, starting with `txid2697049`, with the SRR number above.

(Click [here](https://www.ncbi.nlm.nih.gov/sra/?term=SRR14253446) if you have trouble)

Study the results page.
Click on the link starting with "SRR..." in the table at the bottom. This takes you to the SRA run browser. Here you can see more information about the data files.

```diff
! "Spots" is the number of sequenced reads (it refers to the read clusters on the sequencing array). Write down how many reads (spots) have been sequenced for your sample and the size of the file.
````  

Click on the tab "Data access". Here, under 'Original format', you can find download links to the two paired fastq files:

<img src="/images/sra_run_browser.png" width="700" height="500">   

Click [here](https://trace.ncbi.nlm.nih.gov/Traces/sra/?run=SRR14289348) if you can't find the right links.  

Right click on the first link to the fastq file (ending with `.gz`) and copy the link. In the terminal where you have logged into the server (!) type the command `wget` and paste the link. Something like this: `wget https://sra-pub-sars-cov2.s3.amazonaws.com/sra-src/SRR14253446/TX-UTA-000336_L001_R1.fastq.gz.1`. Press enter. This should download the first fastq file. Do the same for the second. After this is done type `ls`. You should now have two new files ending with `fastq.gz.1`.  


## Decompress the fastq files
The `.gz` in the filename indicates that the files are compressed using the gzip program. Before we can decompress them we have to change their name so that it does end in `.gz` instead of `.gz.1`. Rename both files accordingly.

In the the unix module from the first week of this course there was an exercise about uncompressing `.gz` files. Use the information there to uncompress both files.

After this is done type `ls` again. You should now have two new files ending with `.fastq`.  

[Back to top](#contents)
