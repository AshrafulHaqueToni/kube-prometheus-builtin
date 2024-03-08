# kube-prometheus-builtin

```json
apply grafana.yaml, kube-state-metrics.yaml
apply prom-configmap.yaml,prom-rbac.yaml,prom-svc.yaml,prom-deployment.yaml
```
```json
kubectl port-forward -n monitoring service/grafana 3000:80
kubectl port-forward -n monitoring service/prometheus 9090
```

#### then create api key from grafana and add in grafana-singlestore.yaml and modify db name and namespace ####


```helm
helm upgrade -i panopticon appscode/panopticon -n kubeops --create-namespace --version=v2024.2.5 \
                             --create-namespace \
                             --set monitoring.enabled=true \
                             --set monitoring.agent=prometheus.io/builtin \
                             --set-file license=kubedb-license-file.txt
```

```helm
helm upgrade -i  kubedb-grafana-dashboards /home/appscodepc/go/src/kubedb.dev/installer/charts/kubedb-grafana-dashboards/ -n kubeops --create-namespace --version=v2024.2.14 --values ./grafana-singlestore.yaml
```
