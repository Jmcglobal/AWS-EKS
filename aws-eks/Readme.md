### TOOLS INSTALLATION

#### AWS CLI 
```
Use Docs:
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
```

#### Kubectl:
```
Use docs:
https://kubernetes.io/docs/tasks/tools/
```
#### Eksctl:
```
Use docs:
https://eksctl.io/installation/
```
#### Install Docker:
```Use Docs:
https://docs.docker.com/desktop/
```

## KUBERNETES COMMANDS:

#### Kubernetes cheet sheet commands docs
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

#### Create cluster control plane without node group
eksctl create cluster --name=my-cluster --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup

#### Get list of cluster
eksctl get cluster

#### List Node group in a cluster
eksctl get nodegroup –cluster=my-cluster

#### eksctl get nodegroup –cluster=my-cluster
kubectl get nodes -o wide

#### View Config Context
kubectl config view –minify


#### Create & Associate IAM OIDC provider for EKS cluster
###### To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create &  associate OIDC identity provider
 eksctl utils associate-iam-oidc-provider --region us-east-1 --cluster my-cluster --approve

#### Create Node Group with additional Add-Ons in public Subnets
```
asg-access
external-dns-access
full-ecr-access
appmesh-access
alb-ingress-access

```
eksctl create nodegroup --cluster=my-cluster \
 --region=us-east-1 --name=eks-node --node-type=t3.medium \
 --nodes=2 --nodes-min=2 --nodes-max=4 --node-volume-size=20 \
--ssh-access --ssh-public-key=virginia --managed --asg-access \
--external-dns-access --full-ecr-access --appmesh-access --alb-ingress-access

#### DELETE CLUSTER AND NODE GROUPS
##### Delete Nodegroup
eksctl delete nodegroup –cluster=<"cluster-name> –name=<"nodegroup-name>

#### Delete cluster
eksctl delete cluster <"cluster-name>

## KUBERNETES IMPERATIVE COMMANDS

#### Create Pod
 kubectl run kubenginx --image stacksimplify/kubenginx:1.0.0

#### Create pod
kubectl get pods

#### Describe a pod
kubectl describe pod <"pod-name>

#### Delete Pod
kubectl delete pod <"pod-name>

#### Expose pod service
kubectl expose pod <"pod-name> --type=<"types either ClusterIP or NodePort> --name=<"service-name> --port <"port-number from 30000>

#### Get pods log
kubectl logs <"pod-name>

#### Stream pods logs
kubectl logs -f <"pod-name>

#### Run Commands inside the pod
kubectl exec -it <"pod-name> ls
kubectl exec -it <"pod-name> env
kubectl exec -it <"pod-name> cat /usr/share/nginx/html/index.html

#### ReplicaSet

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: hello
  labels:
    app: hello
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello
  template:
    metadata:
      labels:
        app: hello
    spec:
      containers:
      - name: hello-world
        image: jmcglobal/custom-nginx:latest  
        imagePullPolicy: IfNotPresent
```
#### Apply rs yaml file
kubectl create -f replicaset.yaml

#### Expose ReplicaSet Service imperative command
kubectl expose rs <"replicaset-name> --type NodePort --port <"container-port-number> --name rs-svc

#### Delete replicaset
kubectl delete rs <"rs-name>

## DEPLOYMENT

```
Ceate Deployment to rollout ReplicaSet
Updating The Deployment
Rolling Back a Deployment
Scaling a Deployment
Pausing and Resuming a Deployment
Deployment Status
Clean up Policy
Canary Deployment
```

#### Create a Deployment
kubectl create deployment <"deployment-name> --image=stacksimplify/kubenginx:1.0.0 

#### Scale Deployment
kubectl scale --replicas=3 deploy/<"deployment-name>

#### Expose deployment as a service
kubectl expose deployment <"deployment-name> --type NodePort --port <"container-port> --name <"service-name>

#### Update the Deployment to new Version of image
kubectl set image deployment/<"deployment-name>  <"container-name> <"image-name>

#### Verify Rollout Status
kubectl rollout status deploy/<"deploy-name>

#### Roll BAck to Previous Version
kubectl rollout undo deploy/<"deploy-name>

### View deployment history revision
kubectl rollout history deploy/<"deploy-name>

#### Roll back deployment to specific revision
kubectl rollout undo deploy/<"deploy-name> --to-revision=<"number>

#### Update Deployment using edit command
kubectl edit deployment <"deploy-name>

#### Restart Deployment
kubectl rollout restart deploy/<"deployment-name">

#### Pause Ddeployment  
```
Once you pause rollout deployment, nothing will happen if any chnages is been made on pause mode.

kubectl rollout pause deploy <deployment-name>

```

#### Set resources limits on containers
kubectl set resources deploy <"deploy-name"> -c=kubenginx --limits=cpu=200m,memory=500Mi

#### Delete Deployment
kubectl delete deploy <"deployment-name>

