# k3s



# [установка helm]
```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```
---

# [добавление нода в кластер]
```
k3s_url="https://k3sm1:6443"
k3s_token="K1035c9d25e79f07306f1c72a8b07c46c3e2d7f2dbd341bd6504f721d63417b708c::server:deefa828359a8b412cde7e17569a4b75"
curl -sfL https://get.k3s.io | K3S_URL=${k3s_url} K3S_TOKEN=${k3s_token} sh - 
```
---

# [подготовка]11
```
sudo apt update && sudo apt upgrade -y
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
sudo ufw allow 6443/tcp
sudo ufw allow 443/tcp
sudo apt install mc
sudo apt install htop
sudo apt install net-tools
sudo apt install ansible
sudo apt install python3
sudo apt install autoremove
sudo systemctl reboot
```
---

# [перезагрузка]12
```
sudo systemctl reboot
```
---

# [правим хост]
```
sudo nano /etc/hosts
172.16.10.3 master
172.16.10.4 worker01
172.16.10.10 worker02
```
---

# [установка k3s-master]
```
curl -sfL https://get.k3s.io | sh -
/etc/systemd/system/multi-user.target.wants/k3s.service → /etc/systemd/system/k3s.service.
```
# [когда поставится увидим]
```
[INFO] systemd: Starting k3s
```
---
# {проверка}
```
systemctl status k3s
```
---

# [добавляем в LENS ли RANCHER]
```
sudo cat /etc/rancher/k3s/k3s.yaml
```
---

# [смотрим токен авторизации]
```
sudo cat /var/lib/rancher/k3s/server/node-token
```
---

# [добавление нода в кластер]
```
k3s_url="https://k3sm1:6443"
k3s_token="K1035c9d25e79f07306f1c72a8b07c46c3e2d7f2dbd341bd6504f721d63417b708c::server:deefa828359a8b412cde7e17569a4b75"
curl -sfL https://get.k3s.io | K3S_URL=${k3s_url} K3S_TOKEN=${k3s_token} sh - 
```
---
```
sudo kubectl cluster-info
```
---
```
sudo crictl ps
```


---
---
---

***

## важные команды

***

## показываеют всю информацию про текущий кластер
```
kubectl get all
```

## сетевые адреса управляющего кластера
```
kubectl cluster-info
```

## Вывести все поддерживаемые типы ресурсов, включая API-группу, флаг namespaced (организован ли ресурс в пространство имён или нет) и Kind
```
kubectl api-resources
```

## показать объединённые настройки kubeconfig
```
kubectl config view
```

## показать список контекстов
```
kubectl config get-contexts
```
## Вывести все сервисы в пространстве имён
```
kubectl get services
```

## Вывести все ноды во всех пространств имён
```
kubectl get nods --all-namespaces
```

## Вывести все поды во всех пространств имён
```
kubectl get pods --all-namespaces
```

## Вывести постоянные тома (PersistentVolumes)
```
kubectl get pv
```

## Показать метки всех подов (или любого другого объекта Kubernetes, которым можно прикреплять метки)
```
kubectl get pods --show-labels
```

## Проверить содержимое объекта
```
kubectl describe <>
```

## получить список событий
```
kubectl get events
```

## Вывод логов в поде <pod-name> в режиме реального времени. Это похоже на команду 'tail -f' Linux.
```
kubectl logs -f <pod-name>
```

