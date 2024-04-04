# kube-prometheus-builtin

### Apply necessary resources for builtin ###
```bash
kubectl apply -f grafana.yaml -f kube-state-metrics.yaml
kuebctl apply -f prom-configmap.yaml -f prom-rbac.yaml -f prom-svc.yaml -f prom-deployment.yaml
```

### Port forwarding for grafana and prometheus ###
```bash
kubectl port-forward -n monitoring service/grafana 3000:80
kubectl port-forward -n monitoring service/prometheus 9090
```

#### then create api key from grafana and add in grafana-singlestore.yaml and modify db name and namespace ####

### install panopticon ###

```helm
helm upgrade -i panopticon appscode/panopticon -n kubeops --create-namespace --version=v2024.2.5 \
                             --create-namespace \
                             --set monitoring.enabled=true \
                             --set monitoring.agent=prometheus.io/builtin \
                             --set-file license=kubedb-license-file.txt
```
### Add Grafana Dashboard for SingleStore ###
```helm
helm upgrade -i  kubedb-grafana-dashboards /home/appscodepc/go/src/kubedb.dev/installer/charts/kubedb-grafana-dashboards/ -n kubeops --create-namespace --version=v2024.2.14 --values ./grafana-singlestore.yaml
```
