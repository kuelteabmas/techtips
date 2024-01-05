# Kubernetes Notes

# Commands

### List
List all nodes
`kubectl get nodes`

List all services in all namespaces in our cluster
`kubectl get svc --all-namespaces -o wide`

List all middleware
`kubectl get middleware`


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


