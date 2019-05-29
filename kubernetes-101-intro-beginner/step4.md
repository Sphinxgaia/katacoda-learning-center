## Kubernetes' useful commands

Here, you will find some basics command.

By default, Kubernetes doesn't have any network. You have to install one :
- In the `HOST 1 Terminal`
  - `curl https://docs.projectcalico.org/v3.6/getting-started/kubernetes/installation/hosted/kubernetes-datastore/calico-networking/1.7/calico.yaml -O`{{execute HOST1}}
  - `kubectl apply -f calico.yaml`{{execute HOST1}}

Wait few minutes that install finishes. All nodes must have STATUS `Ready`
- In the `HOST 1 Terminal`
  - `kubectl get node`{{execute HOST1}}

### Pratice

#### List

List all Kubernetes Objects :
- In the `HOST 1 Terminal`
  - `kubectl api-resources`{{execute HOST1}}

List specific type of object :
- In the `HOST 1 Terminal`
  - `kubectl get [ OBJECT NAME ] [OPTIONS]`

List node :
- In the `HOST 1 Terminal`
  - `kubectl get node`{{execute HOST1}}
  - `kubectl get node -owide`{{execute HOST1}}
  
List namespace :
- In the `HOST 1 Terminal`
  - `kubectl get namespaces`{{execute HOST1}}
  - `kubectl get ns`{{execute HOST1}}
  
List pods :
- In the `HOST 1 Terminal`
  - `kubectl get pods`{{execute HOST1}}
  - `kubectl get po`{{execute HOST1}}
  
List all apps ressources in a specific namespaces :
- In the `HOST 1 Terminal`
  - `kubectl get all`{{execute HOST1}}
  - `kubectl get all -n kube-system`{{execute HOST1}}


#### Pod

Create pod (default ns is `default`) :
- In the `HOST 1 Terminal`
  - `kubectl run test -it --image=sphinxgaia/training-centos:latest`{{execute HOST1}}
  - `exit`{{execute HOST1}}
  - `kubectl get po`{{execute HOST1}}

Interact (execute command in pod with interactive mode) :
- In the `HOST 1 Terminal`
  - `kubectl exec -it $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') -- bash`{{execute HOST1}}

Logs (logs container, if multiple you must indicate which container's logs you want see):
- In the `HOST 1 Terminal`
  - `kubectl logs $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}

Describe (pods deployment - node placement, and other info) :
- In the `HOST 1 Terminal`
  - `kubectl describe po $(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`{{execute HOST1}}
  
Delete (delete pod - by default run a pod create associate deployment) :
- In the `HOST 1 Terminal`
  - `kubectl delete deploy test`{{execute HOST1}}

---

> You can't run Kubernetes command on worker.
> 
> All commands : https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands