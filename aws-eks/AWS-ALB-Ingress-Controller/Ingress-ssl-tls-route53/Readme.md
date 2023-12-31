## SSL-TLS

- Register a domain on route53

- Create Certificate using ACM (*global.com), this will match any subname. eg food.global.com, chess.global.com | you don't need to create any subdomain certificate on ACM

- Add Ingress SSL-TLS anotations;

```
 ## SSL Settings
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTPS":443}, {"HTTP":80}]'
    alb.ingress.kubernetes.io/certificate-arn: <certifcate-arn>

```
- Apply all the yaml files

- Go to route53, and create a subdomain reecord, alias, and point it to ingress load-balancer

- Access it with https://food.clobal.com/<path> | If your ingress rules is path pattern