# DRI-ARC (Digital Research Alliance Canada)


This repository provides a step-by-step guide to using Compute Canada's HPC resources for running Python scripts via job submission. It includes:

1. Creating an account on the Digital Research Alliance of Canada platform.
2. Connecting to clusters via SSH.
3. Transferring files between your local machine and the cluster.
4. Writing and submitting Slurm job scripts.
5. Monitoring and troubleshooting jobs.


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

