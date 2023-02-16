## Deploy Cluster

[https://github.com/kubernetes-sigs/kubespray/tree/v2.18.2](https://github.com/kubernetes-sigs/kubespray/tree/v2.18.2)

```bash
ansible-playbook -i inventory/mycluster/inventory.ini --become --become-user=root --ask-become-pass --user=user_name cluster.yml
```


## Вариант создания kubeconfigfile №1

Нужно создать service account.
создать cluster role binding 
сформировать kubeconfigfile самостоятельно.
Команды выполнятся на мастер ноде.
Для создания service account необходимо выполнить команды:

```bash
sudo /usr/local/bin/kubectl create serviceaccount super-admin -n kube-system
sudo /usr/local/bin/kubectl create clusterrolebinding super-admin --clusterrole=cluster-admin --serviceaccount=kube-system:super-admin
```

Для получения токена.
```bash
sudo /usr/local/bin/kubectl get serviceaccounts super-admin -o yaml -n kube-system
sudo /usr/local/bin/kubectl describe secret -n kube-system "полученый токен"
```

Для получения certificate-authority-data.
```bash
sudo /usr/local/bin/kubectl config view --flatten --minify
```

## Вариант создания kubeconfigfile №2

```bash
kubectl apply -f create_account.yml
kubectl discribe  -n (namespace) secret (name_secret)
```