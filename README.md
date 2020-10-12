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

## Task 3 (Prometheus, Grafana)

- Устанавливаем prometheus-operator

``kubectl create namespace monitoring``

``helm install prom stable/prometheus-operator -f prometheus/prometheus.yaml -n monitoring``

 - Отключаем ingress и устанавливаем свой, для сбора метрик
 
 ``minikube addons disable ingress``
 
 ``helm install nginx stable/nginx-ingress -f ingress/nginx-ingress.yaml -n monitoring --atomic``

- Устанавливаем приложение

``kubectl create namespace myapp``

``helm install myapp ./app -n myapp``

- Прокидываем порты для доступа к Prom. и Graf.

``kubectl config set-context --current --namespace=monitoring``

``kubectl port-forward service/prom-grafana 9000:80``

``login: admin password: prom-operator``

``kubectl port-forward service/prom-prometheus-operator-prometheus 9090``

## Task 5 (auth)

- Создаем namespace

``kubectl create namespace app``

``kubectl config set-context --current --namespace=app``

- Устанавливаем helm с auth сервисом

``helm dependency build services/auth``

``helm install auth services/auth -n app``

- Устанавливаем helm с user сервисом

``helm install user services/user -n app``


