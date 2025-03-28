# Contents
- [Find data](#find-data)
- [Download data to the server](#download-data-to-the-server)

## Find data  
First, make sure you have done the instructions described in [00-Get_started.md](00-Get_started.md).  

Then create a folder on your home area called `Module10` and enter it. We will do all the exercises inside this folder.  

As you have probably learned, there are many databases for HTS data. The two most common and comprehensive are probably [ENA - the European Nucleotide Archive](https://www.ebi.ac.uk/ena/browser/home) and the [NCBI SRA database](https://www.ncbi.nlm.nih.gov/sra).

We will use SRA today and download some public HTS data from SARS-CoV-2, the Covid-19 virus. Click on the SRA link above and type in "SARS-CoV-2" in the search box. You should now be on a page looking something like this:  
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

At the top of the page, in the search bar, replace what is there with the SRR number above.

(Click [here](https://www.ncbi.nlm.nih.gov/sra/?term=SRR14253446) if you have trouble)

Study the results page.
Click on the link starting with "SRR..." in the table at the bottom. This takes you to the SRA run browser. Here you can see more information about the data files.

```diff
! "Spots" is the number of sequenced reads (it refers to the read clusters on the sequencing array). Write down how many reads (spots) have been sequenced for your sample and the size of the file.  
````  
  
The SRA database stores data in files ending with .sra. These needs to be downloaded using something called the [SRA-Toolkit](https://hpc.nih.gov/apps/sratoolkit.html). Use this command: (The argument `--split-3` splits the file so that reads for pair 1 and pair 2 ends up in different files). 

`fastq-dump SRR14253446 --split-3 --gzip`

 You should now have two new files ending with `fastq.gz`.  

The `.gz` in the filename indicates that the files are compressed using the gzip program. Fastq files are often large, and it's a good idea to keep them compressed to save space. Most bioinformatics tools can handle compressed files directly. If you need to decompress the files, you can use the `gunzip` command. And if you want to inspect the files in the terminal you can use a combination of `zcat` and `less`.

[Back to top](#contents)
