# README
The following guide is a demonstration purposes only and should not be used in a production environment. 

# Prerequisites
The following can be installed on MacOS using `brew`
- [kustomize](https://kustomize.io/) <= 4.5.2
- [kubectl](https://kubernetes.io/docs/tasks/tools/) <= 1.24.3 
- [kind](https://kind.sigs.k8s.io/) <= 0.14.0

# Getting Started 
### Create a local Kubernetes cluster using kind
```
$ kind create cluster --name grafana-stack-demo --image kindest/node:v1.24.2 --config kind.yaml
```

### Verify cluster is healthy
```
$ kubectl get nodes
```

### Deploy Grafana, Prometheus, Loki, Podinfo, TeslaFi, Pronestheus
```
$ kustomize build apps/dev/ | kubectl apply -f -
```

### Port-forward to Grafana
```
$ kubectl port-forward deployment/grafana 3000:3000
```

### Login to Grafana on Browser
```
http://localhost:3000
```

### Import Dashboard into Grafana
Go to Dashboards on the `Grafana Console` and import the 2 JSON dashboards found in `/apps/base/grafana/dashboards`.

### Terminate the Cluster
```
$ kind delete cluster --name grafana-stack-demo   
```

# Troubleshooting

If metrics are not showing up, verify that Prometheus are able to scrape the pods properly. 
# Port-forward to Prometheus
`$ kubectl port-forward deployment/prometheus-deployment 9090:9090`