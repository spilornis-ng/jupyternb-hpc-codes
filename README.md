# jupyternb-hpc-codes
Codes to run Jupyter Notebook via HPC tunneling

#First login to your HPC account user@hpc

#Start an interactive job session on the HPC

[user@masternode ~]$ qsub -I -l select=1:ncpus=40,pmem=46,walltime=2:00:00 -N jobname -q queuename

#At this stage you will shift from masternode to a single node allocated for your job (example, xyz@masternode to xyz@node02 - here you have shifted from master node to node 02 on the HPC)
#Note the IP address of this node

[user@node02 ~]$ hostname -i

#You can now start a Jupyter notebook session using the following code

[user@node02 ~]$ Jupyter notebook --no-browser --port=<portno> --ip=$(hostname -i) 

#Here you can assign any port no which you want to tunnel via (for example, 8800). However, if the port is busy then the notebook will start with next available port no. You can note the portno from the on screen dialogue

#Your jupyter notebook session with the allocated resources will be now running
#To start the notebook session in the web browser run the following code in a new terminal on the local machine (your laptop/pc)

[user@Desktop]$ ssh -NL <yourlocalportno>:xx.yy.zz.aaa:<portno> user@hpc #example ssh -NL 1111:10.10.10.102:8888 user@iisert

#You can now enter the your localportno in a web browser to start a remote Jupyter notebook session on the HPC remotely

https://localhost:1111

#It might ask you token number or password. If you have setup a password for your Jupyter notebook, you can enter it here. Otherwise, the token can be located on the on screen dialogue one you run the Jupyter notebook command
