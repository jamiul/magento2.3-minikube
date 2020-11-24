

## Installation

### Requirements
- [x] Docker
- [x] Kubernetes
- [x] Minikube
- [x] Kubectl
### Clone Repository
Clone the source locally:

```sh
$ git clone https://github.com/jamiul/magento2.3-minikube.git
$ cd <folder_name>
```
`Create secretKeyRef`:
You have to convert username and password base64.
To make base64 try this command.

```sh
$ echo -n 'username' | base64
$ echo -n 'password' | base64
```

Apply secret file.

```sh
$ kubectl apply -f mysql-scret.yaml
$ kubectl get secret // get secret file
```

### Deploying MySQL

Create mysql-deployment yaml file
```sh
$ kubectl apply -f <your mysql deployment yaml file>
$ kubectl get services
$ kubectl get pods
```
Go to Mysql bash and login as mysql root user
```sh
$ kubectl exec -it <pod name> -- /bin/bash
$ mysql -u root -p
```
Display databases
```sh
$ mysql -uroot -p${MYSQL_ROOT_PASSWORD} -e 'show databases;'
```
### Magento Deployment
Display databases
```sh
$ kubectl apply -f <magento deployment yaml file>
```
Go to magento bash
```sh
$ kubectl exec -it <magento pod name> -- /bin/bash
```
Download magento2.3 via composer
```sh
$ composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition:2.3 <directory name>
```
 Install via CLI
 ```sh
 $ bin/magento setup:install \
--base-url=http://192.168.49.2:31657 \
--db-host=magento2-mysql \
--db-name=root_magento2 \
--db-user=root \
--db-password=password \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1

 ```
 Run magento
```sh
$ minikube service <service name>
```
