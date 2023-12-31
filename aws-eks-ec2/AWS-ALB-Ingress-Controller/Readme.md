### WHAT IS ALB

ALB is  asuper advanced next-generation load balancer in AWS, support for path-based routing, (/app1, /app2, /usermgmt).

It also support for Host-based routing ( app.global.com, users.mikel.com).

Support for routing based on fields in the request (HTTP Headers, HTTP Methods, Query parameters and Source IP Address).

Support for redirecting requests from one URL to another.

Support for returning a custom HTTP response.

Support for registering Lambda functions as targets.

Support for the Load Balancer to authenticate users of your applications through their corporate or social identities before routing requests.

Support for containerized applications (AWS ECS).

Support for Monitoring the health of each service independently, as health checks are defined at the target group level.

Support for registering targets by IP address, includng targets outside the VPC for the load balancer.

#### ALB is the latest load balancer with many good features

## ALB INGRESS CONTROLLER

Ingress controller triggers the creation  of an Application Load Balancer (ALB) and the necessary supporting AWS resources whenever an ingress resource is created on the cluster with the kubernetes,io/ingress.class: alb annotation

## References: 
- Good to refer all the below for additional understanding.

### ALB Pre-requisite Setup - References: 
- https://github.com/kubernetes-sigs/aws-alb-ingress-controller
- Examples:
  - https://github.com/kubernetes-sigs/aws-alb-ingress-controller/tree/master/docs/examples/2048

### AWS ALB Ingress Annotations Reference
- https://kubernetes-sigs.github.io/aws-alb-ingress-controller/guide/ingress/annotation/

### eksctl getting started
- https://eksctl.io/introduction/#getting-started

### External DNS
- https://github.com/kubernetes-sigs/external-dns
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/alb-ingress.md
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md

#### ALB INGRESS CONTROLLER TYPES

##### Instance Mode
```Registers nodes within your cluster as targets for the ALB.
* traffic reaching the ALB is routed to NodePort for your service and then proxied to pods ( Default traffic mode)
* This is not support on fargate type, you must use IP mode on fargate cluster
```
#### IP Mode
```Registers pods as targets for the ALB
* Traffic reaching the ALB is directly routed to pods for your service.
* Supported on fargate cluster, because there is no node to managed on AWS fargate
```

### AWS Load Balancer Controller
- [AWS Load Balancer Controller Documentation](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/)


### AWS ALB Ingress Annotations Reference
- https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/annotations/

### eksctl getting started
- https://eksctl.io/introduction/#getting-started

### External DNS
- https://github.com/kubernetes-sigs/external-dns
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/alb-ingress.md
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md