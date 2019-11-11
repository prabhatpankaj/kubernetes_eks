export nodecount=1

# Friendly name for your cluster
export CLUSTER_FULL_NAME="ekslab"

* Creating an EKS cluster

We use eksctl to create and EKS cluster using one line command.

```
eksctl create cluster --name=${CLUSTER_FULL_NAME} --nodes=${nodecount} --region=${AWS_DEFAULT_REGION}

```
