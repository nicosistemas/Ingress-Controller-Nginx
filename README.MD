## Instalación:

Para configurar un Ingress Controller en AWS configuraremos un Ingress Nginx "nlb-with-tls-termination" pues se necesita https. El archivo ingress-nginx.yaml del repo que ya contiene todas las configuraciones deployará todo lo necesario.


Datos a tener en cuenta:
* Configurar Certificados Tls:
Agregar el arn para nuestro certificado en "service.beta.kubernetes.io/aws-load-balancer-ssl-cert: arn:aws:acm:us-west-2:XXXXXXXX:certificate/XXXXXX-XXXXXXX-XXXXXXX-XXXXXXXX", borrar el item   proxy-real-ip-cidr: XXX.XXX.XXX/XX y pasar a "false" el item "use-forwarded-headers"
Una vez deployado todo el stack "Ingress-Nginx" resta aplicar nuestro Ingress (ingress-monitoring.yaml) que contiene todas las URLs: prometheus, grafana, alertmanager.
* Matching:
La forma que tiene el Ingress Controller Nginx de saber a que servicios (URLs) apuntar de nuestro ingress monitoring es mediante el ingressClassName: nginx

### fuentes:
https://github.com/kubernetes/ingress-nginx/blob/main/deploy/static/provider/aws/nlb-with-tls-termination/deploy.yaml
https://kubernetes.io/docs/concepts/services-networking/ingress/
https://kubernetes.github.io/ingress-nginx/deploy/#network-load-balancer-nlb
https://github.com/dolguin-/aws101-kubernetes/blob/main/clase-9/readme.md