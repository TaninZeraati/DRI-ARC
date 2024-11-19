# DRI-ARC (Digital Research Alliance Canada)


This repository provides a step-by-step guide to using Compute Canada's HPC resources for running Python scripts via job submission. It includes:

1. Creating an account on the Digital Research Alliance of Canada platform.
2. Connecting to clusters via SSH.
3. Transferring files between your local machine and the cluster.
4. Writing and submitting Slurm job scripts.
5. Monitoring and troubleshooting jobs.

> **Note**: This guide is intended as an introductory resource to demonstrate the basic steps for connecting to and using HPC clusters. It provides sample workflows for new users.

---

## **Getting Started**

## **1. Creating an Account**

To access the advanced research computing resources provided by the Digital Research Alliance of Canada, you need to create an account.

1. Visit the account registration page:  
   [Apply for an Account](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account)

3. **Steps to Apply**:
   - Log in using your institution's credentials (e.g., through a university login system).
   - Complete the account application form, including:
     - Your research project details.
     - Supervisor or sponsor information (Note that you need a sponsor (such as supervisor) for getting resources).
   - Wait for approval. You’ll receive an email with your account credentials once approved.

4. Once your account is active, proceed to connect to a cluster.

---

## **2. Connecting to a Cluster**

### **What is a Cluster?**
- A **cluster** is a group of interconnected computers used for high-performance computing.
- Each cluster consists of:
  - **Login Nodes**: Where users log in to access the cluster.
  - **Compute Nodes**: Machines that perform the actual computations.
  - **Scheduler**: A system that manages job execution on the cluster.

### **How to Connect**
Use the `ssh` command to log in to a cluster. Replace `<username>` with your Alliance account username and `<cluster_name>` with the cluster's hostname.

```bash
ssh <username>@<cluster_name>.computecanada.ca
```

Example:
```ssh okpas30@beluga.computecanada.ca```
On your first login, you may need to accept the server’s fingerprint by typing yes and set extra information.

## **3. Transferring Files

### **From Local Machine to Server**
Use the `scp` (Secure Copy Protocol) command:

```bash
scp <path_to_local_file> <username>@<cluster_name>.computecanada.ca:/User/remote/directory
```

Example: ```scp Downloads/samplefile.py okpas30@beluga.computecanada.ca:/home/okpas30/```

### **From Server to Local Machine**
To copy files from the server to your local machine:

```bash
scp <username>@<cluster_name>.computecanada.ca:/path/to/remote/file <path_to_local_directory>
```

Example: ```scp okpas30@beluga.computecanada.ca:/home/okpas30/bertexperimentieee.py ~/Downloads/```

## **4. Writing a Slurm Job Script
### **What is a Job?**
- A **job** is a task or series of tasks submitted to the cluster for execution.
- Jobs are managed by a scheduler, such as Slurm, which ensures efficient resource allocation.

### **Sample Slurm Job Script**
Create a file called `submit_job.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=python_job          # Job name
#SBATCH --output=job_output.txt        # Output file
#SBATCH --time=00:10:00                # Runtime limit (HH:MM:SS)
#SBATCH --ntasks=1                     # Number of tasks
#SBATCH --cpus-per-task=1              # CPUs per task
#SBATCH --mem=2GB                      # Memory allocation

# Load necessary modules
module load python/3.8

# Run the Python script
python samplefile.py

```

## **5. Submitting a Job**
Submit your job script using the `sbatch` command:
```bash
sbatch submit_job.sh
```
A Job Id will be assigned to this job.

### **Checking Job Status**
To monitor your job:
```bash
squeue -u <username>
```

### **Canceling a Job**
```bash
scancel <job_id>
```


## **6. Monitoring Output**
After your job completes, view the output file specified in your job script (e.g., `job_output.txt`):
```bash
cat job_output.txt
```

## **7. Viewing Available Partitions**

To see the partitions (queues) available on the cluster:
```bash
sinfo
```

Example output:
```bash
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
compute   up     7-00:00:00    50   idle compute[01-50]
gpu       up     2-00:00:00    10   idle gpu[01-10]

```

## **Common Errors and Fixes**
1. **Partition Error:**
   If you encounter:
   ```bash
   sbatch: error: The specified partition does not exist

   ```
   - Remove the `#SBATCH --partition` line from your job script.

2. **Python Module Not Found:**
   - Search for the correct version of python.
   - Load the correct Python module:
   ```bash
      module load python/3.8

   ```
