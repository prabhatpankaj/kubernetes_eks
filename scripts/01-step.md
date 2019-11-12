# EKS CLUSTER CREATION WORKFLOW

![EKS CLUSTER CREATION WORKFLOW](images/eks-customers.svg)

# WHAT HAPPENS WHEN YOU CREATE YOUR EKS CLUSTER

![WHAT HAPPENS WHEN YOU CREATE YOUR EKS CLUSTER](images/eks-k8s-control-plane.svg)

# EKS ARCHITECTURE FOR CONTROL PLANE AND WORKER NODE COMMUNICATION

![EKS ARCHITECTURE FOR CONTROL PLANE AND WORKER NODE COMMUNICATION](images/eks-architecture.svg)

# HIGH LEVEL
Once your EKS cluster is ready, you get an API endpoint and you’d use Kubectl, community developed tool to interact with your cluster.

![HIGH LEVEL](images/eks-high-level.svg)

# Create an EKS cluster

export nodecount=1

* Friendly name for your cluster

export CLUSTER_FULL_NAME="ekslab"

* Creating an EKS cluster

We use eksctl to create and EKS cluster using one line command.

```
eksctl create cluster --name=${CLUSTER_FULL_NAME} --nodes=${nodecount} --region=${AWS_DEFAULT_REGION}

```

* Deleteing an EKS cluster

```
eksctl delete cluster --name=${CLUSTER_FULL_NAME}

```
