<!--- app-name: etcd Defragmentation CronJob Helm Chart -->

# Introduction 

This Helm chart deploys a etcd instance with CronJob for defragmenting an etcd cluster. 
Regular defragmentation helps maintain the performance and efficiency of the etcd cluster 
by reclaiming storage space and optimizing the database. 
The CronJob is configured to run daily at midnight.

# Setup Instructions

# Prerequisites
1.Kubernetes Cluster: Ensure you have a running Kubernetes cluster.
2.Helm: Helm should be installed and configured on your system.
3.kubectl: Make sure kubectl is installed and configured to interact with your Kubernetes cluster.

# Deployment Steps

- $git clone https://github.com/meirmany/Cynomi-TASK.git
- $cd Cynomi-TASK/Task-1
- $helm install my-etcd ./etcd-10.2.11.tgz --namespace <namespace_name>

# Configuration Options

The values.yaml file contains several configurable parameters:

- cronjob.schedule: The schedule for running the CronJob (e.g., "0 0 * * *" for daily at midnight).
- cronjob.resources: Resource requests and limits for the CronJob container.
- image.registry: The container registry for the etcd image.
- image.repository: The repository for the etcd image.
- image.tag: The tag of the etcd image.

# Defrag CronJob

The defrag CronJob dynamically discovers the etcd endpoints within the Kubernetes cluster 
and performs defragmentation on these endpoints. 
This ensures that the defragmentation process is always up-to-date with the current cluster configuration.

# Additional Features or Improvements

1. Scalability -->
   The CronJob dynamically adjusts to the number of etcd endpoints discovered in the cluster, 
   making it suitable for scaled environments.

2. Monitoring and Alerts -->
   Integrate monitoring tools (for example Prometheus) 
   to track the health and performance of the etcd cluster and the CronJob.

3. Backup -->
   Add a backup to complement the defrag process, to ensure  data safety and recoverability in case of failures.

4. Resource Optimization -->
   Fine-tune resource requests and limits for better resource management 
   and to prevent overconsumption of cluster resources.

