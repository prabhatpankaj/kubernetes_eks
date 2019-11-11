# Setting up a workstation in AWS
* From which we can create and interact with EKS cluster.

* Launch an EC2 instance as a workstation

Provisioning an EC2 instance in AWS as a workstation to manage all AWS resources including EKS.
Login to the AWS console and launch an Amazon Linux EC2, ssh login then configure AWS CLI, then we can start to install kubectl and eksctl.

* Install kubectl

```
sudo apt-get update && sudo apt-get install -y apt-transport-https

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

sudo apt-get install -y kubectl

```

* Download aws-iam-authenticator

```
curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.11.5/2018-12-06/bin/linux/amd64/aws-iam-authenticator

chmod +x ./aws-iam-authenticator

mkdir bin

cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$HOME/bin:$PATH

```

* Install eksctl

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

```

* Install awscli

```
sudo apt  install awscli

export AWS_DEFAULT_REGION=us-east-1

```

* Set up the initial IAM policies for the eks user

```
aws iam create-group --group-name eksuser

aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess

aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess

aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonVPCFullAccess

aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/IAMFullAccess

aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonRoute53FullAccess
    
aws iam attach-group-policy --group-name eksuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryFullAccess
    
aws iam create-user --user-name eksuser

aws iam add-user-to-group --user-name eksuser --group-name eksuser

aws iam create-access-key --user-name eksuser >eksuser-creds

cat eksuser-creds

sudo apt  install jq

export AWS_ACCESS_KEY_ID=$(cat eksuser-creds | \
    jq -r '.AccessKey.AccessKeyId')

export AWS_SECRET_ACCESS_KEY=$(cat eksuser-creds | \
    jq -r '.AccessKey.SecretAccessKey')

aws ec2 create-key-pair --key-name ekslab \
    | jq -r '.KeyMaterial' >ekslab.pem

chmod 400 ekslab.pem

```
