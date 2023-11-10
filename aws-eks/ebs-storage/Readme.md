### EBS CSI Driver Installation 
```
Create IAM policy for EBS
Associate IAM policy to worker Node IAM Role
Install EBS CSI Driver
```

#### Create IAM Policy

Policy 

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:CreateSnapshot",
        "ec2:CreateTags",
        "ec2:CreateVolume",
        "ec2:DeleteSnapshot",
        "ec2:DeleteTags",
        "ec2:DeleteVolume",
        "ec2:DescribeInstances",
        "ec2:DescribeSnapshots",
        "ec2:DescribeTags",
        "ec2:DescribeVolumes",
        "ec2:DetachVolume"
      ],
      "Resource": "*"
    }
  ]
}
```

### Use kubectl command get IAM role policy of EKS worker node
kubectl -n kube-system describe configmap aws-auth

### Associate the policy to the WorkerNode IAM role
Use aws Console

#### Deploy EBS CSI Driver
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=master"

## Use AWS docs for EBS CSI Driver
https://docs.aws.amazon.com/eks/latest/userguide/csi-iam-role.html

```
eksctl create iamserviceaccount \
    --name ebs-csi-controller-sa \
    --namespace kube-system \
    --cluster <cluster-name> \
    --role-name AmazonEKS_EBS_CSI_DriverRole \
    --role-only \
    --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
    --approve
```

#### Adding the Amazon EBS CSI driver add-on (AmazonEKS_EBS_CSI_DriverRole is a role name)
eksctl create addon --name aws-ebs-csi-driver --cluster "cluster-name" --service-account-role-arn arn:aws:iam::<"aws accound ID">:role/AmazonEKS_EBS_CSI_DriverRole --force

#### Remove EBS CSI Driver
eksctl delete addon --cluster "cluster-name" --name aws-ebs-csi-driver --preserve

### Note
```
StorageClass 
PersistentVolumeCliam
ConfigMap
mysql deployment
mysql service deployment
```
### User management frontend to test the mysql
```
deploying the usermgmt to test the mysql, once its connected it will be running
endpoint = :<port-number/usermgmt/health-status>

It will respond with <User Management Service UP and RUNNING - V1>

```
```
Access the mysql databases

kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql  -pdbpassword11

```