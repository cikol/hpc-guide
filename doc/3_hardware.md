# HPC hardware specifications
RTU HPC cluster “Rudens” consists of 54 computing nodes for job execution and one head node which performs cluster management function. All nodes are inter-connected with fast InfiniBand network. Each compute node is equipped with two x86_64 architecture processors (CPUs), and some of the nodes additionally with 2 or 4 Nvidia Tesla graphical accelerators (GPU). Cluster architecture is heterogeneous, combining nodes of different generations and technical parameters.

Several network-attached storage systems are available for storing user data with a total capacity of ~800 TB. For tasks with intensive I/O, a special NVMe disk array with BeeGFS parallel file system is available.

Users connect to a separate login node which provides a work environment and tools for running jobs in the cluster. Job management is provided by Torque/Moab tools.

![alt text](./images/data_center.jpg)

General System parameters:
- 54 computing nodes
- 1200+ CPU cores
- 8 TB RAM (up to 1.5 TB per process)
- 16 Graphical Nvidia Tesla processors (GPU)
- 132 TFlops overall performance (62 Tflops x86 + 70 Tflops GPU)
- 800 TB data storage
- 10 Gb/s access network
- 40-100 Gb/s InfiniBand interconnection

## Access Network
10 Gbps connection with Latvian Academic computer network, European Academic Computer Network GEANT, Genomics Data Network, and 2 Gbps to commercial Internet providers in Latvia is provided.

##HPC cluster “Rudens”
### Login nodes
- ui-2.hpc.rtu.lv (primary): 2 x AMD EPYC 7502P (Rome) @ 2.5GHz (kopā 64 kodoli), RAM 256 GB DDR4, 3.5 TB NVMe RAID 0, 100 Gb/s Ethernet piekļuves tīkls, 100 Gbiti/s Infiniband EDR
- ui-1.hpc.rtu.lv: 2 x Intel Xeon CPU E5-2680 v3 @ 2.50GHz (total 24 cores), 128 GB RAM, 10 Gb/s Ethernet access network, 56 Gb/s InfiniBand FDR 
### CPU computing nodes
- 3 nodes AMD Dell EMC PowerEdge R6525, (wn62-wn64, feature=epyc): 2 x AMD Epyc 7713 (Milan) @ 2 GHz (total 128 cores per node), RAM 512 GB DDR4, 3.5 TB NVMe RAID 0, 100 Gbiti/s Infiniband EDR
- 10 nodes Dell EMC PowerEdge R640 (wn02-wn10, feature=vasara): 2 x Intel(R) Xeon(R) Gold 6154 CPU @ 3.00GHz (total 36 cores per node), RAM 384 GB DDR4 2666 MHz ECC, 1TB SSD, Infiniband EDR 100 Gb/s
- 11 nodes Dell PowerEdge R630 (wn45-wn55, feature=rudens): 2 x Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz (total 24 cores per node), RAM: 128 GB DDR4 2133MHz ECC, 200 GB SSD, Infiniband FDR 56 Gb/s
### GPU computing nodes
- 1 GPU mezgls Lenovo SR670 V2 (wn44, feature=lenovo,a100):2 x Intel Xeon Gold 6348 gen.3 @ 2.6Hz (total 56 cores per node),4 x NVIDIA A100 GPU, 40 GB HBM2, NVLink, 512 GB DDR4 3200 MHz ECC, 5.8 TB NVMe SSD, Infiniband EDR 100 Gb/s
- 2 GPU mezgli Dell EMC PowerEdge C4140 (wn59-wn60, feature= vasara,v100): 2 x Intel(R) Xeon(R) Gold 6130 CPU @ 2.10GHz (total 32 cores per node), 4 x NVIDIA Tesla V100 GPU uz mezglu, 16 GB HBM2, 5120 CUDA kodoli, 192 GB DDR4 2666 MHz ECC, 240 GB SSD, Infiniband EDR 100 Gb/s
- 4 GPU mezgli Dell PowerEdge R730 (wn43,wn56-wn58, feature= rudens,k40): 2 x Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz (total 24 cores per node), 2 x NVIDIA Tesla K40 GPU uz mezglu, 12GB GDDR5, 2888 CUDA kodoli, RAM 128 GB DDR4 2133MHz ECC, 200 GB SSD, Infiniband FDR 56 Gbiti/s
### High memory nodes
- 1 node Dell PowerEdge R940 (wn01): 4 x Intel Xeon Gold 6140 CPU @ 2.30GHz (total 72 cores per node), RAM 1.5 TB DDR4 2666 MHz ECC, 1TB SSD, InfiniBand EDR 100 Gb/s
### Cluster management software
- Operating system (OS): Linux Centos 7.9
- Job Management: Torque 6.1.1.1/ Moab 9.1.1
- Accounting: Moab Accounting Manager
- OS image provisioning: xCAT

## Data Storage Systems
### NFS network data storage (238 TB, /home) 
- 8 nodes EMC Isilon x200 
-	Distributive file system OneFS, 
-	client connection with NFS protocol  
-	40 Gb/s InfiniBand connection with the cluster
-	238 TB SATA SDD + SATA Spinning disks  
### BeeGFS network data storage #2 (430 TB, /home_beegfs; /scratch_beegfs) 
-	2 nodes SuperStorage 6029P 
-	Parallel file system BeeGFS 
-	100Gbit/s Infiniband  
-	30TB NVMe fast disk pool
-	400 TB NL SAS disk pool
### BeeGFS network data storage #1 (104 TB, /mnt/beegfs) 
-	2 nodes: SuperStorage 6029P and Lenovo x3650 M5  
-	Parallel file system BeeGFS 
-	10 Gb/s  Infiniband with cluster 
-	100 TB SATA HDD disk pool 
### Scratch disks (15 TB in total) 
-	Computing nodes are equipped with local SDD disks with capacity up to 3.5 TB

## Node names
| Name | Type | RAM  | CPU |	CPU cores |	GPUs | 	Local disk | qsub features |
| ---- | ---- | ---- | --- | --------- | ---- | ----------- | ------------- |
| rudens | cluseter head | 32 GB | E5-2620 v3 |  |  |  | 
| ui-1 | login | 64 GB | E5-2650 v3 | 20 | 0 | /scratch | 
| ui-2 | login | 256 GB | EPYC 7502P | 64 | 0 | /scratch | 
| wn01 | compute-smp, high-mem | 1.48 TB | Gold 6140 | 72 | 0 | /scratch | dell vasara highmem centos7 largescratch |
| wn02-wn11 | compute | 384 GB | Gold 6154 | 36 | 0 | /scratch | dell vasara centos7 largescratch gold6154 |
| wn45-wn55 | compute | 128 GB | E5-2680 v3 | 24 | 0 | /scratch | dell rudens centos7 |
| wn44 | compute-gpu | 512 GB | Gold 6348 | 56 | 4 | /scratch, 5.8 TB | lenovo gpu a100 |
| wn43, wn56-wn58 | compute-gpu | 128 GB | E5-2680 v3 | 24 | 2 | /scratch | dell rudens gpu k40 centos7 |
| wn59-wn60 | compute-gpu | 192 GB | Gold 6130 | 32 | 4 | /scratch | vasara vasara-32 gpu v100 centos7 |
| wn61 | compute, high-mem | 2 TB | Epyc 7F72 | 48 | 0 | /scratch, 1.8 TB | epyc7f72 largescratch |
| wn62-wn64 | compute | 512 GB | Epyc 7713 | 128 | 0 | /scratch, 3.5 TB | epyc epyc7713 centos7 |
