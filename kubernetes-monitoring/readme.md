### Мониторинг Kubernetes
1. Для примера взял из прошлых ДЗ образ nginx, модифицировал конфиг
1. Так же модифицировал один из прошлых Deployment nginx, добавив туда sidecar контейнер с nginx-exporter
2. Prometheus Operator был установлен из helm chart, в отредактированными values.yaml

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm upgrade --install kube-prometheus-stack prometheus-community/kube-prometheus-stack -f values.yaml \
 --set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false \
 --set prometheus.prometheusSpec.podMonitorSelectorNilUsesHelmValues=false
```

3. Переменные были установлены в false согласно статье
> [https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack#prometheus-io-scrape]
> By default, Prometheus discovers PodMonitors and ServiceMonitors within its namespace, that are labeled with the same release tag as the prometheus-operator release. 
> Sometimes, you may need to discover custom PodMonitors/ServiceMonitors, for example used to scrape data from third-party applications. An easy way of doing this, without compromising the default PodMonitors/ServiceMonitors discovery, is allowing Prometheus to discover all PodMonitors/ServiceMonitors within its namespace, without applying label filtering. 
> To do so, you can set prometheus.prometheusSpec.podMonitorSelectorNilUsesHelmValues and prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues to false.

4. К сожалению, не смог понять, почему Prometheus не видит Service Monitor для моего сервиса.