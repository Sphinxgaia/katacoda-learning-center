## Kubernetes' useful commands

Here, you will find some basics command.

By default, Kubernetes doesn't have any network. You have to install one :
- `curl https://docs.projectcalico.org/v3.6/getting-started/kubernetes/installation/hosted/kubernetes-datastore/calico-networking/1.7/calico.yaml -O`{{execute HOST1}}
- `kubectl apply -f calico.yaml`{{execute HOST1}}

Wait few minutes that install finishes. All nodes must have STATUS `Ready`
- `kubectl get node`{{execute HOST1}}

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
- `kubectl get all -n kube-system`{{execute HOST1}}


#### Pod

Create pod (default ns is `default`) :
- `kubectl run test -it --image=sphinxgaia/training-centos:latest`{{execute HOST1}}
- `exit`{{execute HOST1}}
- `kubectl get po`{{execute HOST1}}

Interact (execute command in pod with interactive mode) :
- `kubectl exec -it $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') -- bash`{{execute HOST1}}

Logs (logs container, if multiple you must indicate which container's logs you want see):
- `kubectl logs $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}

Describe (pods deployment - node placement, and other info) :
- `kubectl describe po $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}
  
Delete (delete pod - by default run a pod create associate deployment) :
- `kubectl delete deploy test`{{execute HOST1}}

---

All commands : https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands