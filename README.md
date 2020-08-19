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


