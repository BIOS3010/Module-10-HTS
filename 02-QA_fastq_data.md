# Contents
- [Inspect the fastq files](#inspect-the-fastq-files)
- [Remove adapters and low quality bases](#remove-adapters-and-low-quality-bases)

## Inspect the fastq files

Use basic Linux commands and your knowledge about the fastq file format to answer the following questions (and save screen shots of how you found the answer):
```diff
! How may lines does the two fastq files contain?
! How many paired reads are in your files? Does this match with the number you found in the previous exercise?
! What is the quality symbol (ASCII character) for the first nucleotide in the first read in the SRR..._1.fastq file?
````
See [this page](https://help.basespace.illumina.com/files-used-by-basespace/quality-scores)   
```diff
! Can you trust that this nucleotide has been called correctly? Explain why.
```
<br>

Now we will run the program [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) (remember to run module load first) which is a quick and easy way to get basic statistics and lots of useful information about our sequence data. Run the command `fastqc SRR14253446_*.fastq` (you know what the wildcard (`*`) does right?)  (NB: Remember to activate the Module10 conda environment first: `conda activate Module10`)

You should see an output like this:  
```
(Module10) [jonbra@bioint02 Module10]$ fastqc SRR14253446_*
application/gzip
application/gzip
Started analysis of SRR14253446_1.fastq.gz
Approx 5% complete for SRR14253446_1.fastq.gz
Approx 10% complete for SRR14253446_1.fastq.gz
Approx 15% complete for SRR14253446_1.fastq.gz
Approx 20% complete for SRR14253446_1.fastq.gz
...
```

FastQC will produce two types of files. `.html` files and `.zip` files. We only need the html files. But since we can't view these files in the terminal you need to download them to your computer.

<!--
(you also did this in [Module 5](https://github.com/BIOS3010/Module-5-multiple-alignment#533-moving-files-from-an-external-server-to-your-own-computer)).-->
<!-- Now changed as we need to go through login.uio.no -->

If you have GitBash, or you have a Mac or Linux machine, you need to open a new terminal window. In the newly opened terminal window you will be on your local computer/laptop (!).
Navigate to, or create, an appropriate folder to store the files you will download today, and in the coming weeks.  

First, on the *server* terminal, type `pwd` to display the path to you location and `ls` to find the name of the file(s) to copy. Then, in the other terminal window which is on *your local machine*, type the following command
* replace *username* with your uio username
* replace *path/to/fastq/file* with the output from `pwd`:    

```bash
scp -J <username>@login.uio.no '<username>@bioint02.hpc.uio.no:path/to/fastq/file/*.html' .
```

NOTES
* The command has both `login.uio.no` and the `bioint02` servers as we need to go through the first one to get access to the second one.
* The dot `.` at the end indicates 'the current folder' as destination.
*  The quotation marks around `username@bioint02.uio.no:path/to/fastq/file/*.html` are needed on some operating systems to make sure the dilcard expnasion `*` works.

Type your UiO password.

Double click the two `.html` files to open them in a web browser. You should see something like this:

<img src="/images/fastqc.png"> <br>   

Not all the information here is relevant for us today. But look at the information in "Basic Statistics", "Per base sequence quality" and "Adapter Content" and answer the following questions:  

**NB! For some reason it seems like NCBI/SRA has changed the quality encoding so that all nucleotides have the same quality score of 30 (or "?" in the fastq file). Therefore, the quality score graph in the html file is not very informative. You can look at the image above instead.**

```diff
! How many sequences/reads are in your file? Is this what you expected?
! How long are they?
! Briefly describe the distribution of quality scores. Is the quality equally good along the entire sequence? Are there any differences in quality between pair 1 and pair 2 reads?
! Are there any sequencing adapters present?
! What are sequencing adapters and how did they get into your data?
```


[Back to top](#contents)


## Remove adapters and low quality bases  

The next thing we need to do is to remove sequencing adapters and low quality bases. We will use a program called [fastp](https://github.com/OpenGene/fastp) for this task. Fastp will automatically detect and remove the most commonly used sequencing adapters. In addition it will remove low quality bases from both ends of the reads. 

```bash
fastp \
-i SRR14253446_1.fastq.gz \
-I SRR14253446_2.fastq.gz \
-o SRR14253446_1_trimmed.fastq.gz \
-O SRR14253446_2_trimmed.fastq.gz
```

Fastp will print some information about the run to the screen.
```diff
! How many paired reads were present after trimming?
! How many reads were removed?
```  

<br>  

**Run FastQC again on the trimmed reads and download the resulting html files to your computer.**  


Answer the following questions:
```diff
! How many sequences/reads are in your trimmed files? Is this what you expected?
! How long are the reads?
! Do they have the same lengths as before trimming? If not, why?
! What has happened to the distribution of quality scores compared to before Trimmomatic?
! Are there any adapters present?
! Why did we do this trimming step?
```

[Back to top](#contents)
