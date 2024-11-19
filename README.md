# DRI-ARC
Step-by-step instruction of how to connect and use digital research alliance canada

README.md
# HPC Job Submission Guide on Compute Canada Clusters

This repository provides a step-by-step guide to using Compute Canada's HPC resources for running Python scripts via job submission. It includes:

- Instructions for connecting to the cluster.
- Managing files between your local machine and the server.
- Writing and submitting Slurm job scripts.
- Monitoring and debugging jobs.

---

## **Getting Started**

### **1. Connecting to the Cluster**
Use the `ssh` command to log in to the cluster. Replace `<username>` with your Compute Canada username and `<cluster_name>` with the name of the cluster (e.g., `beluga`).

```bash
ssh <username>@<cluster_name>.computecanada.ca
Example:
ssh okpas30@beluga.computecanada.ca
2. Transferring Files
From Local to Server
Use the scp command to copy files from your local machine to the server. Replace <path_to_local_file> with the file path on your machine and <username> and <cluster_name> as above.
scp <path_to_local_file> <username>@<cluster_name>.computecanada.ca:/path/to/remote/directory
Example:
scp Downloads/samplefile.py okpas30@beluga.computecanada.ca:/home/okpas30/
From Server to Local
To copy files from the server to your local machine:
scp <username>@<cluster_name>.computecanada.ca:/path/to/remote/file <path_to_local_directory>
Example:
scp okpas30@beluga.computecanada.ca:/home/okpas30/bertexperimentieee.py ~/Downloads/
3. Writing a Slurm Job Script
A Slurm job script specifies how your job will run on the cluster. Below is a sample script:
submit_job.sh
#!/bin/bash
#SBATCH --job-name=python_job          # Job name
#SBATCH --output=job_output.txt        # Standard output and error log
#SBATCH --time=00:10:00                # Runtime limit (HH:MM:SS)
#SBATCH --ntasks=1                     # Number of tasks (processes)
#SBATCH --cpus-per-task=1              # CPUs per task
#SBATCH --mem=2GB                      # Memory per node

# Load necessary modules
module load python/3.8

# Run your Python script
python samplefile.py
Save this script as submit_job.sh.
4. Submitting a Job
Submit your job script using the sbatch command:
sbatch submit_job.sh
5. Monitoring Jobs
Use the following commands to monitor your jobs:
Check the Status of Your Jobs:
squeue -u <username>
Example:
squeue -u okpas30
Cancel a Job:
scancel <job_id>
Example:
scancel 12345
6. Job Output
After the job completes, the output and error logs will be saved in the file specified by the #SBATCH --output directive (e.g., job_output.txt). View the output with:
cat job_output.txt
7. Available Partitions
To see available partitions (queues) and their configurations:
sinfo
8. Example Workflow
Here’s a quick workflow for running a Python script:
Upload Your Python Script:
scp samplefile.py okpas30@beluga.computecanada.ca:/home/okpas30/
Write a Job Script: Save the following as submit_job.sh:
#!/bin/bash
#SBATCH --job-name=python_job
#SBATCH --output=job_output.txt
#SBATCH --time=00:10:00
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=2GB

module load python/3.8
python samplefile.py
Submit the Job:
sbatch submit_job.sh
Monitor the Job:
squeue -u okpas30
View Output:
cat job_output.txt
Common Errors and Fixes

Partition Not Found:
Remove the #SBATCH --partition line from your job script.
File Not Found:
Double-check the file paths in the scp command or in the job script.
Python Module Not Found:
Load the correct Python module using module load python/3.8.
Repository Contents

samplefile.py: A sample Python script for testing.
submit_job.sh: A Slurm job script template.
README.md: This guide.
Contact

For questions or issues, contact [your email] or your system administrator.

---

### **Next Steps**
1. Save this content in a file named `README.md`.
2. Place `samplefile.py` and `submit_job.sh` in your repository as examples.
3. Push the repository to GitHub:
   ```bash
   git init
   git add README.md samplefile.py submit_job.sh
   git commit -m "Add HPC job submission guide"
   git remote add origin <your_repo_url>
   git push -u origin main
Let me know if you want me to create additional sample files or scripts!
