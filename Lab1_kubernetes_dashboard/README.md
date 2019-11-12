#  DEPLOY THE KUBERNETES DASHBOARD

![Dashboard](/images/dashboard.png)

* The official Kubernetes dashboard is not deployed by default, but there are instructions in the official documentation.

We can deploy the dashboard with the following command:

```
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.8.3.yaml 

```

* Go to URL that got created:To get the URL:

```
kubectl cluster-info
```

Example URL:
https://api-yoururl.amazonaws.com

* Open url 

```
https://api-yoururl.amazonaws.com/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/overview?namespace=default

```
* To create a service account with access to default namespace

```
kubectl create serviceaccount dashboard -n default

```  
  
* To create a cluster role bind. Connecting service account and cluster level access

```
kubectl create clusterrolebinding dashboard-admin -n default \
--clusterrole=cluster-admin \
--serviceaccount=default:dashboard

```

* To get the login token that you will be asked on the URL:

```
kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode 

```
* Default login credentials you can get by using following kops command in terminal:
Username: admin
Password: (using command)

```
aws eks get-token --cluster-name ${CLUSTER_FULL_NAME} | jq -r '.status.token'

```
