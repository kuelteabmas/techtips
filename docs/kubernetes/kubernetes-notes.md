# Kubernetes Notes

# Commands

### Restart

Restart a deployment
`kubectl rollout restart deployment/nginx`

____

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

List all challenges (Let's Encrypt ACME Certificates)
`kubectl get challenges`


____

### Logs

View logs continuously (tailing)
`kubectl logs -n namespace_name -f pod_name`
`kubectl logs -n cert-manager -f cert-manager-79497589cf-kk2mb`

___

### Describe
Print out the deployment in question 
`kubectl describe deployment nginx` 

Print out the service in question 
`kubectl describe service nginx` 

Describe ingressroute ingressroutes.traefik.containo.us
`kubectl describe ingressroutes.traefik.containo.us`

___

### Delete

Delete a deployment
`kubectl delete deployment deployment_name`

Deleted all Succeeded and Completed pods in all namespaces 
`kubectl delete pods --field-selector status.phase=Succeeded --all-namespaces`

Deleted all Failed and Evicted pods in all namespaces 
`kubectl delete pods --field-selector status.phase=Failed --all-namespaces`

___

### Applying files

Apply a file
`kubectl apply -f example.yml` 

Apply a folder containing .yaml files

example: 
***nginx folder contains 3 files:***

```
nginx
   ├── deployment.yaml
   ├── ingress.yaml
   └── service.yaml
```

`kubectl apply -f nginx`

___

### Namespaces

Create a namespace
`kubectl create namespace namespace_name`


___

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

___
