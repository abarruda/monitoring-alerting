## Deployment

```bash
$ helm repo add stable https://charts.helm.sh/stable
$ helm dependency update 
```
```
helm upgrade --install --debug \
--set grafana.service.loadBalancerIP=192.168.1.123 \
--set prometheus.server.retention=14d \
--set prometheus.alertmanagerFiles."alertmanager\.yml".global.smtp_smarthost=smtp.host.com:26 \
--set prometheus.alertmanagerFiles."alertmanager\.yml".global.smtp_from=alerts@host.com \
--set prometheus.alertmanagerFiles."alertmanager\.yml".global.smtp_auth_username=alerts@host.com \
--set prometheus.alertmanagerFiles."alertmanager\.yml".global.smtp_auth_password=pass123! \
--set prometheus.alertmanagerFiles."custom-templates\.tmpl"="\{\{ define \"smtp_to\" \-\}\}email\@address.com\{\{\- end\}\}" \
--set prometheus.alertmanager.service.loadBalancerIP=192.168.1.456 \
--set prometheus.server.service.loadBalancerIP=192.168.1.789 \
monitoring-alerting .
```

### Caveats

Sidecar loading/reloading of dashboards in ConfigMaps would be preferred but the ```kiwigrid/k8s-sidecar:0.1.20``` container does not currently have an ARMv7 version.  Dashboards are loaded from the JSON files in the ```dashboard``` directory in this project, instead of residing with the projects they are designed for.

#### Resources

https://raw.githubusercontent.com/carlosedp/cluster-monitoring/master/grafana-dashboards/kubernetes-cluster-dashboard.json