Here we want to introduce you the main concept of Sequence Alignment and Multiple Sequence Alignment. The tool T-Coffee and a bit of Nextflow.

Welcome to this tutorial.
----------
Tutorial
----------

----------
Hands ON
----------
We have a container with T-Coffee to avoid instalation issues and configurations. Just to see what is inside the container and the "raw" T-Coffee. We will go inside the container and see how it looks like.
```
cd container
docker run -it cbcrg/some_name
```
Now we are inside the container. It's a container with all ready for run TC.
We have a couple of dummy sequences to play.
```
cd tcoffee
t_coffee -seq SH3_aa.fa -run_name=SH3_tcoffee
```
Lets explain what we did.
We call TC with a sequence input and we defined a name for the output.
TC returns 3 files. A tree (.dnd), an alignment (.aln) and a html file where we can see the alignment with the color code we explain before.

Let's take a look. Just type the next commands
```
#To see how the tree looks like. (We will see after a fancy way to read it)
cat SH3_tcoffee.dnd

#Let's check the alignment
cat SH3_tcoffee.aln

#Presualice the html file
firefox SH3_tcoffee.html
```

As we saw, we can run different modes in TC, lets try one of them and we are finish inside the container.
```
t_coffee -seq SH3_aa.fa -mode mcoffee -run_name=SH3_mcoffee
```
We can see how the command it's quite similar but we introduce the flag ```-mode``` and we define a proper output name to identify the outputs.

Let's close the container and perform more operations
```exit```

Now, we will use Nextflow (Di Tommaso, Paolo et al 2017) to perform the following experiments. We will explain the basics to run TC.
Before start, we need to check the configuration file. This si the place where we indicate the container to use with all the tc installation.
```cat nextflow.config```

Let's take a look to the first script ```tc-ex1.nf```
Here we can see the ***channels*** that they are the input/output of our program.
In this first example, we recollect the fasta files '''*.fa''' from the folder ```/seqs/*.fa```
And the output we will place on the directory ```/results```

The command line we will run in this case is the easy example we did before:
```
t_coffee -seq ${seqs} -run_name=${id}_tcoffee
```

Then, let's do the same we did before inside the container, but from NextFlow to see what are the differences.
```
nextflow run tc-ex1.nf
```
Now, time to check the ```results``` folder and we will see the same 3 files for each fasta file (seatoxin and SH3_aaa). As we can see, the results are the same as the previous job submission, but in this case with just one click we have done two jobs in paralel.

Move on, and let's go to the second script.
In this case we will try to run different modes and other functionalities, let's take a look.
Open the file ```vim tc-ext2.nf``` and take a look.
In this case we will run t-coffee but with the use of the modes. In the proccess coffee_flavour we can find all the different methods to align sequences.





