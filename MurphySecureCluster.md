# Running Code on the Secure Cluster
Harvard Research Computing provides shared computing resources through Odyssey. Why should you use Odyssey? Reasons include...

* Need to run code for many hours, and it's too annoying to run it on your laptop
* Need to run a bunch of code in parallel (e.g. fit a model using 100 different hyper-parameters)
* Need access to GPUs

If you are interested in using Odyssey to run code on publicly available data (i.e. test sets from UCI), you can start [with the general Quickstart guide](https://docs.rc.fas.harvard.edu/kb/quickstart-guide/). There is a plethora of great resources out there you can use to familiarize yourself with running things on the cluster!

<mark>This tutorial focuses specifically on running code on the Murphy lab's **secure** cluster.</mark> Hopefully you know whether or not your data is elligable to run in the main cluster (if it's secure, you most likely signed some sort of confidentiality agreement). Please check with Susan/Jess before transferring data to any clusters!

Before you get started, please make sure to create an Odyssey account under the Murphy lab group (instructions in the general Quickstart tutorial above).

## Joining the correct groups
You will need to send Jess an email with your Odyssey account username and ask to be added to the following groups: 
1. **vpn_murphy**: lets you connect to a certain "realm" on the VPN which tunnels into the secure cluster
2. **murphy_secure**: lets you log into the secure cluster
3. ***<the group for the specific dataset you will work with>***: for example, to work with the Heartsteps data you will be added to "murphy_s_heartsteps"

Make sure to be added to all three groups! The Harvard RC team may add you only to (3), the group for the specific dataset you will work with. But you need all three in order to access the relevant resources. 

## Running jobs from the cluster
Once you have permissions, you are ready to log into the cluster.

### 1. Join the VPN
You will need to set up your laptop to work with [Harvard's VPN system](https://docs.rc.fas.harvard.edu/kb/vpn-setup/). The Cisco Anyconnect Client will ask for the following fields: 

* Connect to: `vpn.rc.fas.harvard.edu`
* Username: `<your username>@murphy`
* Password: `<your password>`
* Second Password: `<your duo mobile auth code>`

Note the realm. When accessing the general VPN, you may have used something like `jharvard@odyssey`. The `@murphy` realm lets you access the secure cluster. 

### 2. Navigating the secure cluster
* You can login on the terminal with the following: `ssh <your username>@murphy-login.rc.fas.harvard.edu
* Once you are logged in, navigate to the `murphy_secure` folder: `cd /n/murphy_secure`
* You can now access the safe folder for the relevant dataset. For example, Heartsteps users will go to the `Heartsteps` folder. If you can't access the intended folder, you will have to ask Jess for read/write access to that specific Murphy group. 

### 3. Submitting jobs
Jobs on the secure cluster must be submitted to the `murphy_secure` partition! By design, I don't think you can run interactive jobs in the secure cluster. All jobs must be submitted in batch. Your settings will look something like this: 

```
#!/bin/bash
#SBATCH -n 1 # Number of cores
#SBATCH -N 1 # Ensure that all cores are on one machine
#SBATCH -t 0-10:00 # Runtime in D-HH:MM
#SBATCH -p murphy # odyssey partition
#SBATCH --mem=10000 # Memory pool for all cores (see also --mem-per-cpu)
#SBATCH -o EXPDIR/out_%j.txt # File to which STDOUT will be written
#SBATCH -e EXPDIR/err_%j.txt # File to which STDERR will be written
```

Make sure to output your results to the `/n/murphy_secure` folder! 

<mark>Missing: information on murphy_secure GPUs and interactive jobs</mark>

## Mounting the secure cluster to your laptop

?? I have not gotten this to work yet. 
