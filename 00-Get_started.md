## Contents
- [Logging on to the server](#logging-on-to-the-server)
- [Installing and using software on a Linux system](#installing-and-using-software-on-a-linux-system)


## Logging on to the server
For this part of the course we will be using a common server with a Linux operating system.
A 'server' is a computer that is located elsewhere, and that you can access remotely over the internet.
Servers are often more powerful, and/or have more memory and storage space than desktop or laptop computers.
Using such Linux servers is thus common in bioinformatics.

### Step 1: logging on to login.uio.no

For security reasons, we cannot log into the the server directly. First, we need to log in to another server called `login.uio.no`.
We used this server earlier in the course.
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
On windows we recommend that you install [GitBash](https://gitforwindows.org/). This gives you a terminal with unix-style commands available on your local machine. You can then log on to the `login.uio.no` server with the same commands as above.  

You should see a message `Welcome to login.uio.no!`

## Logging on to the analysis server

Once you are logged in to `login.uio.no`, you can log in to the analysis server:

* **odd-numbered groups (1, 3, 5, ...)** do this: `ssh username@itf-appn-test01.hpc.uio.no`
* **even-numbered groups (2, 4, 6, ...)** do this `ssh username@itf-appn-test02.hpc.uio.no`

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

[Back to top](#contents)


## Installing and using software on a Linux system
Installing software on a Linux server like the ones we are using in this class can sometimes be difficult. Many programs have "dependencies", other programs or libraries, that needs to be installed in a specific way in order for the program to run properly. On the servers that we are using in this course there are many programs that have been pre-installed.

* The command `module avail` will give you a list of all pre-installed software. This list is very long. If only the first few are listed (you do not see the prompt (`$`) at the bottom):
  * to browse through, use the spacebar
  * to go back to the terminal prompt, press the `q` key
* To activate a specific program, run `module load software_name/version`

For the rest of the HTS module, we will use `fastqc` and `trimmomatic`. Here, we will only test that you can load the corresponding modules and test the progam.

For `fastqc`, run:

```
module load FastQC/0.11.9-Java-11
fastqc --version
```

You should see this as output:
```
FastQC v0.11.9
```

Now we do the same for Trimmomatic: use `module avail trimmomatic` to figure out the installed version(s). If there is more than one, use the latest version.
Load the module and *read the instructions on how to use the program carefully!* Find out which version we are using by running trimmomatic with `-version` as only parameter.


[Back to top](#contents)
