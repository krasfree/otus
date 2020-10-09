## Task 1 (app)
``kubectl apply -f .`` 

## Task 2.1 (statefulset)
``kubectl apply -f .`` 

## Task 2.2 (helm mysql)
``helm repo add bitnami https://charts.bitnami.com/bitnami``

``helm repo update``

``helm install mysql bitnami/mysql -f mysql/values.yaml``

``kubectl apply -f .``

## Task 2.3 (my helm app)

``helm dependency build app/``

``helm install myapp app/``

## Task 5 (auth)

- Создаем namespace

``kubectl create namespace app``

``kubectl config set-context --current --namespace=app``

- Устанавливаем helm с auth сервисом

``helm dependency build services/auth``

``helm install auth services/auth -n app``

- Устанавливаем helm с user сервисом

``helm install user services/user -n app``


