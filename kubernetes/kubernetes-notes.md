# Kubernetes Notes

# Commands

### List
List all nodes
`kubectl get nodes`

List all services in all namespaces in our cluster
`kubectl get svc --all-namespaces -o wide`

List all ingresses
`kubectl get ingressroute`
> `--namespace` | `kubectl get ingress --namespace andromeda`

List all ingress routes
`kubectl get ingressroute`
>`--namespace` | `kubectl get ingressroute --namespace andromeda`


List all middleware
`kubectl get middleware`

List all secrets
`kubectl get secrets`
>`--namespace` | `kubectl get secrets --namespace traefik`


### Describe
Print out the deployment in question 
`kubectl describe deployment nginx` 

Print out the service in question 
`kubectl describe service nginx` 

Delete a deployment
`kubectl delete deployment deployment_name`


Apply a file
`kubectl apply -f example.yml` 


### Namespaces

Create a namespace
`kubectl create namespace namespace_name`


### Definitions

##### CRD or Custom Resource Definitions
CRD defines objects in kubernetes that kubernetes doesn't know about natively.

For instance, whenyou run `kubectl get certificate`, you'll get a response of `error: the server doesn't have a resource type "certificate"
`
Therefore, CRD come into play. 
example: `https://github.com/cert-manager/cert-manager/releases/download/v1.13.3/cert-manager.crds.yaml` 

`kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.3/cert-manager.crds.yaml`

Response:
`No resources found in default namespace.`
