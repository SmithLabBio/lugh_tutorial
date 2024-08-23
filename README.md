# Cisco AnyConnect
Install the Cisco AnyConnect VPN Client.
You will need to use this anytime you want to log onto the cluster through any network other than an ethernet connection on campus.
1. Go to `vpn.msstate.edu`, log in, download the app, and install it.
2. Once installed open the Cisco AnyConnect VPN Client.
3. Enter `vpn.msstate.edu` into the address field and click connect.
4. Enter your username, password, and enter `push` into the `Duo Password` field. Then click ok.
5. Approve the push notification sent through Duo Mobile to your phone. If it does not appear in your notifications you may need to open the Duo Mobile app in order to approve it.

 
# Terminal
### MacOS/Linux
Open a terminal application

### Windows
Open PowerShell



# SSH
### Login Command
```
ssh <net id>@lugh.biology.msstate.edu
```
If you receive the following prompt:
>The authenticity of host ... can't be established.  
>RSA key fingerprint is ...  
>Are you sure you want to continue connecting (yes/no)?  

Enter yes to approve.  
Enter password when prompted.  

### SSH Keys
The login process can be made less cumbersome by using ssh keys.

#### Generate SSH Keys
```bash
ssh-keygen
```
It is not necessary to enter a passphrase. If key already exists type "n" and skip this command.

#### Copy SSH Keys to remote computer
```bash
ssh-copy-id <net id>@lugh.biology.msstate.edu 
```



# Lugh File System
### Home
`/mnt/home/<net id>/` 
This is the current working directory at login. This is intended for storing installations and important files that are not too large in number or size. Space is limited here so be careful to not overload this directory as it may eventually become an issue for all cluster users.

### Scratch
`/mnt/scratch/smithlab/`
This location is intended to be used for storing large files or large numbers of files temporarily. This is a good place to store the output of programs. It should be fine to keep files for a few months but when you no longer need them you should delete them.

### Fast Scratch
`/mnt/scratch/smithfs/`
Another space intended to be used for temporary storage for large files or a large number of files. Reading and writing to this location is much faster than it is in scratch so it is intended for cases where a program is doing frequent reading and writing of data.  

### Symlinks
Symlinks to these directories can be nice to have.
```bash
ln -s /mnt/scratch/smithlab/ /mnt/home/<net id>/scratch 
```



# Slurm
Slurm is the job scheduling software used on Lugh and is used to run jobs on the compute nodes. Run anything that is resource intensive through Slurm and not on the login node as this will interfere with other user's ability to use the system.

### Submitting a job
#### From the command line
```bash
sbatch --job-name test --mem 1G --time 0-01:00:00 --partition smith --cpus-per-task 1 --wrap "echo test; sleep 20; echo done"
```

#### As part of script
Put the following into a file called test.slurm
```bash
#!/bin/bash

#SBATCH --job-name=Test_run_on_OCI
#SBATCH --cpus-per-task=1
#SBATCH --time 0-01:00:00 
#SBATCH --mem 1G
#SBATCH --partition smith 

echo test
sleep 20
echo done
```
Submit the job to the cluster
```bash
sbatch test.slurm
```

### Monitoring
Monitor job progress
```
squeue -u <net id>
```

### Interactive Job
To be able to interact with a job running on the cluster.
```bash
srun --pty bash
```



# Software
The cluster has a number of commonly used programs already installed.

### Available Software
To see what is available:
```bash
module avail
```

### Loaded Software
To see which programs are currently loaded in your environment:
```bash
module list
```

### Load Software
To load a program:
```bash
module load <program name>
```



# Vscode
Microsoft Visual Studio Code is a really nice editor that integrates with the cluster.

### Download
https://code.visualstudio.com/

### Install Extensions
Install the Remote Development Extension
