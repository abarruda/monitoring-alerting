## Deployment
```
helm dependency update
```
```
helm upgrade --install --debug --wait grafana .
```

### Caveats

Sidecar loading/reloading of dashboards in ConfigMaps would be preferred but the ```kiwigrid/k8s-sidecar:0.1.20``` container does not currently have an ARMv7 version.  Dashboards are loaded from the JSON files in the ```dashboard``` directory in this project, instead of residing with the projects they are designed for.

#### Resources

https://raw.githubusercontent.com/carlosedp/cluster-monitoring/master/grafana-dashboards/kubernetes-cluster-dashboard.json