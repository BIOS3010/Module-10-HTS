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
See [this table](https://support.illumina.com/help/BaseSpace_OLH_009008/Content/Source/Informatics/BS/QualityScoreEncoding_swBS.htm)   
```diff
! Can you trust that this nucleotide has been called correctly? Explain why.
```
<br>

Now we will run the program [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) which is a quick and easy way to get basic statistics and lots of useful information about our sequence data. Run the command `fastqc TX-UTA-000336_L001_R*.fastq` (you know what the wildcard (`*`) does right?)  

You should see an output like this:  
```
Started analysis of TX-UTA-000336_L001_R1.fastq
Approx 5% complete for TX-UTA-000336_L001_R1.fastq
Approx 10% complete for TX-UTA-000336_L001_R1.fastq
Approx 15% complete for TX-UTA-000336_L001_R1.fastq
Approx 20% complete for TX-UTA-000336_L001_R1.fastq
...
```

FastQC will produce two types of files. `.html` files and `.zip` files. We only need the html files. But since we can't view these files in the terminal you need to download them to your computer.

<!--
(you also did this in [Module 5](https://github.com/BIOS3010/Module-5-multiple-alignment#533-moving-files-from-an-external-server-to-your-own-computer)).-->
<!-- Now changed as we need to go through login.uio.no -->

If you have GitBash, or you have a Mac or Linux machine, you need to open a new terminal window. In the newly opened terminal window you will be on your local computer/laptop (!).
Navigate to, or create, an appropriate folder to store the files you will download today, and in the coming weeks.  

First, on the *server* terminal, type `pwd` to display the path to you location and `ls` to find the name of the file(s) to copy. Then, in the other terminal window which is on *your local machine*, type the following command (replace *username* with your uio username (group 6-10 use test02 instead of test01) and replace *path/to/fastq/file* with the output from `pwd`):    

```bash
scp -J username@login.uio.no ´username@itf-appn-test01.hpc.uio.no:path/to/fastq/file/*.html´ .
```

NOTES
* The command has both `login.uio.no` and the `itf-appn-test` servers as we need to go through the first one to get access to the second one.
* The dot `.` at the end indicates 'the current folder' as destination.

Type your UiO password.

Double click the two `.html` files to open them in a web browser. You should see something like this:

<img src="/images/fastqc.png"> <br>   

Not all the information here is relevant for us today. But look at the information in "Basic Statistics", "Per base sequence quality" and "Adapter Content" and answer the following questions:

```diff
! How many sequences/reads are in your file? Is this what you expected?
! How long are they?
! Briefly describe the distribution of quality scores. Is the quality equally good along the entire sequence? Are there any differences in quality between pair 1 and pair 2 reads?
! Are there any sequen adapters present?
! What are sequencing adapters and how did they get into your data?
```


[Back to top](#contents)


## Remove adapters and low quality bases  

The next thing we need to do is to remove sequencing adapters and low quality bases. We will use a program called [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic) for this task. Run the following command (it's long so you can copy and paste. Copy all lines together):

```bash
java -jar $EBROOTTRIMMOMATIC/trimmomatic-0.39.jar PE TX-UTA-000336_L001_R1.fastq TX-UTA-000336_L001_R2.fastq \
TX-UTA-000336_L001_R1_trimmed.fastq TX-UTA-000336_L001_R1_unpaired.fastq \
TX-UTA-000336_L001_R2_trimmed.fastq TX-UTA-000336_L001_R2_unpaired.fastq \
ILLUMINACLIP:/storage/software/software/Trimmomatic/0.39-Java-11/adapters/TruSeq3-PE.fa:2:30:10 \
SLIDINGWINDOW:4:20 \
MINLEN:36
```

* `PE` tells Trimmomatic that we have paired reads.
* Then we specify the two input fastq files
* next we tell the program what file names to use for the trimmed paired and unpaired reads (if an entire read is removed from one of the files, then the corresponding read pair in the other file will be put into the "unpaired" files).  
* `ILLUMINACLIP` specifies how adapters will be removed.  
* `SLIDINGWINDOW:4:20` means that Trimmomatic will use a window of 4 bases and cut the read when the average base quality drops below 20.  
* `MINLEN:36` indicates that only reads longer than 36 bp after adapters and low quality bases are removed will be saved.  

Trimmomatic will print some information about the run to the screen.
```diff
! How many paired reads are present after trimming?
! How many sequences were removed?
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
