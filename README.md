# drevofil_platform
drevofil Platform repository
## Знакомство с Kubernetes, основные понятия и архитектура 
> Разберитесь почему все pod в namespace kube-system восстановились после удаления. Укажите причину в описании PR

core-dns - Deployment, который следит за количеством реплик и перезапускает поды при их удалении
kube-proxy - Daemonset, аналогично Deployment следит за работой подов на каждой ноде Kubernetes
kube-apiserver, kube-scheduler, etcd - Static pod, за которыми следит systemd служба kubelet, манифесты хранятся по пути /etc/kubernetes/manifests
storage-provisioner - аналогичный Static pod, является аддоном Kubernetes и его конфиг хранится в /etc/kubernetes/addons