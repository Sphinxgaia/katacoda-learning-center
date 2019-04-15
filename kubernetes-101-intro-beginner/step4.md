## Kubernetes' useful commands

Here, you will find some basics command.

### Pratice

#### List

List all Kubernetes Objects :
- `kubectl api-resources`{{execute HOST1}}

List specific type of object :
- `kubectl get [ OBJECT NAME ] [OPTIONS]`

List node :
- `kubectl get node`{{execute HOST1}}
- `kubectl get node -owide`{{execute HOST1}}
  
List namespace :
- `kubectl get namespaces`{{execute HOST1}}
- `kubectl get ns`{{execute HOST1}}
  
List pods :
- `kubectl get pods`{{execute HOST1}}
- `kubectl get po`{{execute HOST1}}
  
List all apps ressources in a specific namespaces :
- `kubectl get all`{{execute HOST1}}
- `kubectl config view | grep namespace:`{{execute HOST1}}
- `kubectl get all -n kube-system`{{execute HOST1}}


#### Pod

Create pod (default ns is `default`) :
- `kubectl run test -it --image=sphinxgaia/training-centos:latest`{{execute HOST1}}
- `exit`{{execute HOST1}}
- `kubectl get po`{{execute HOST1}}

Interact :
- `kubectl exec -it $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') -- bash`{{execute HOST1}}

Logs :
- `kubectl logs $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}

Describe :
- `kubectl describe po $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}
  
Delete :
- `kubectl delete deploy test`{{execute HOST1}}

---

All commands : https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands