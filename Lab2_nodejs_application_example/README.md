# DEPLOY THE EXAMPLE MICROSERVICES

![MICROSERVICES](/images/microservices.svg)

* DEPLOY NODEJS BACKEND API

```
git clone https://github.com/prabhatpankaj/ecsdemo-nodejs.git

cd ecsdemo-nodejs
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml

```

* We can watch the progress by looking at the deployment status:

```
kubectl get deployment ecsdemo-nodejs

```

* DEPLOY CRYSTAL BACKEND API

```
git clone https://github.com/prabhatpankaj/ecsdemo-crystal.git

cd ecsdemo-crystal
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml

```
* We can watch the progress by looking at the deployment status:

```
kubectl get deployment ecsdemo-crystal

```

* DEPLOY FRONTEND SERVICE

Let’s bring up the Ruby Frontend!

```
git clone https://github.com/prabhatpankaj/ecsdemo-frontend.git
cd ecsdemo-frontend

kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml

```

* We can watch the progress by looking at the deployment status:

```
kubectl get deployment ecsdemo-frontend

```

* SCALE THE BACKEND SERVICES

When we launched our services, we only launched one container of each. We can confirm this by viewing the running pods:

```
kubectl get deployments
```

Now let’s scale up the backend services:

```
kubectl scale deployment ecsdemo-nodejs --replicas=3
kubectl scale deployment ecsdemo-crystal --replicas=3

```

Confirm by looking at deployments again:

```
kubectl get deployments

```
Also, check the browser tab where we can see our application running. You should now see traffic flowing to multiple backend services.

# SCALE THE FRONTEND

Let’s also scale our frontend service the same way:

```
kubectl get deployments
kubectl scale deployment ecsdemo-frontend --replicas=3

```
Confirm by looking at deployments again:

```
kubectl get deployments

```

Check the browser tab where we can see our application running. You should now see traffic flowing to multiple frontend services.

# CLEANUP THE APPLICATIONS
To delete the resources created by the applications, we should delete the application deployments:

Undeploy the applications:

```
cd ecsdemo-frontend
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

cd ecsdemo-crystal
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

cd ecsdemo-nodejs
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

```
