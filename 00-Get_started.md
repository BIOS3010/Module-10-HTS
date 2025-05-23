## Contents
- [Logging on to the server](#logging-on-to-the-server)
- [Installing and using software on a Linux system](#installing-and-using-software-on-a-linux-system)  
- [When logging back on to the server](#when-logging-back-on-to-the-server)


## Logging on to the server
For this part of the course we will be using a common server with a Linux operating system.
A 'server' is a computer that is located elsewhere, and that you can access remotely over the internet.
Servers are often more powerful, and/or have more memory and storage space than desktop or laptop computers.
Using such Linux servers is thus common in bioinformatics.

### Step 1: logging on to login.uio.no

For security reasons, we cannot log into the the server directly. First, we need to log in to another server called `login.uio.no`.
From `login.uio.no`, we can log in to the server for analyses we will do this week and the coming weeks. **Note that from outside the UiO network you need to have [two factor authentication set up](https://www.uio.no/tjenester/it/brukernavn-passord/2fa/)**.

Depending on your operating system there are different ways to log on to the `login.uio.no` server.

**Mac/Linux**  
If you have a Mac or a Linux PC, these already run on a Linux-like Operating System and you can open a program called the **Terminal**. The Terminal gives you access to all Linux commands.

When you have that program open, type

```
ssh username@login.uio.no
```

Replace *username* with your UiO username and hit Enter. Type in your UiO password (NB: you will not see anything happen when you type. This is normal).

<img src="/images/terminal.png" width="400"> <p>
You should see a message `Welcome to login.uio.no!`

Next, see below under "Logging on to the course server".

**Windows**  
If you have a program called **Terminal** installed already, use that one. If not, we recommend that you install [GitBash](https://gitforwindows.org/). This gives you a terminal with unix-style commands available on your local machine. You can then log on to the `login.uio.no` server with the same commands as above.  

You should see a message `Welcome to login.uio.no!`

## Logging on to the analysis server

Once you are logged in to `login.uio.no`, you can log in to the analysis server:

`ssh <username>@bioint02.hpc.uio.no`

You may get a message like this:

```
The authenticity of host ... can't be established.
...
Are you sure you want to continue connecting (yes/no)? yes
```
Type 'yes' and press enter.

Again, write your password when asked for it.

When you have logged on to the server, type the command `pwd`. You should see something like this
<img src="/images/terminal_2.png" width="500" height="300"> <p>  

## Loggin in in one step  
It's also possible to log in to the server via login.uio.no in one single step. But you need to type your password twice.  
`ssh -J <username>@login.uio.no <username>@bioint02.hpc.uio.no`  

[Back to top](#contents)


## Installing and using software on a Linux system
Installing software on a Linux server like the ones we are using in this class can sometimes be difficult. Many programs have "dependencies", other programs or libraries, that needs to be installed in a specific way in order for the program to run properly. On the servers that we are using in this course there are many programs that have been pre-installed.

* The command `module avail` will give you a list of all pre-installed software. This list is very long. If only the first few are listed (you do not see the prompt (`$`) at the bottom):
  * to browse through, use the spacebar
  * to go back to the terminal prompt, press the `q` key
* To activate a specific program, run `module load software_name/version`

For the rest of the HTS module, we will use `sra-tools`, `fastqc` and `fastp`. `sra-tools` and `fastqc` are pre-installed on the server. But unfortunately not `fastp`. In order to install this software we will use `conda`, which is a so-called "package manager". Do the following: 

```bash
# Activate the conda software
module load Miniconda3/4.9.2

# Initialize conda (need only do once)
conda init bash

# Then you need to log out and back in again 

# Create a new environment that will hold software specific for this module
conda create --name Module10
conda activate Module10

# Install fastp
conda install bioconda::fastp
```

And then activate the other software: 
```bash
# First enable software specific for BIOS3010
module use /home/BIOS3010/software/modules/all/:/opt/software/BIOS3010/modules/all/

# See available software
module avail

# Activate the software we need
module load SRA-Toolkit/2.10.9-gompi-2020b
module load FastQC/0.11.9-Java-11
```

[Back to top](#contents)  

## When logging back on to the server  
If you have everything set-up and working on the server, and when you log back on after being logged out you need to do this:  
```bash
# Make sure conda is active
module load Miniconda3/4.9.2

# Activate the conda environment (change the Module10 name is you used a different name)
conda activate Module10

# Activate the BIOS3010 software
module use /home/BIOS3010/software/modules/all/:/opt/software/BIOS3010/modules/all/

# And then load the specific modules you need
module load SRA-Toolkit/2.10.9-gompi-2020b
module load FastQC/0.11.9-Java-11
```

[Back to top](#contents)  
