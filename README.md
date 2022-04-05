# ДЗ *Kubernetes-к8s-*

## Задание:

**1.Ответить на вопросы:**

* Что такое k8s?
> Kubernetes — это открытое программное обеспечение для автоматизации развёртывания, масштабирования и управления контейнеризированными приложениями.

* В чём преимущество контейнеризации над виртуализацией?
> Автоматизация, cкорость создания, экономичность, высокая производительность

* В чём состоит принцип самоконтроля k8s?
> Перезапускает отказавшие контейнеры, заменяети завершает работу контейнеров, которые не проходят определённую пользователем проверку работоспособности

* Как вы думаете, зачем Вам понимать принципы деплоя в k8s?
> Для обеспечения декларативных обновлений для модулей Pod и ReplicaSet. Deployment управляет жизненным циклом приложения и описывает особенности его запуска: сколько реплик требуется запустить, из какого образа, на каких портах, сколько ресурсов необходимо выделить (RAM, CPU), какие Healthcheck можно использовать для проверки работоспособности, какие метки и селекторы применять и т.д.

* Какое из средств управления секретами наиболее распространено в использовании совместно с k8s?
> generic, docker-registry, TLS-сертификаты для Ingres

* Какие типы нод есть в k8s, каковы их базовые функции?
> Master node (управляет кластером и является точкой входа для всех административных задач)
> Worker node (виртуальный или физический сервер, который запускает приложения и управляется главным узлом)

**2.Написать манифест, который будет содержать в себе следующие условия: ● apiVersion – v1 ● название – netology-ml ● внутри него сервер приложений tomcat версии 8.5.69 с портом 8080 ● наличие 2 реплик ● использование стратегии rollingupdate**
---
apiVersion: v1
kind: Deployment
metadata:
  name: netology-ml
spec:
  replicas: 2
  selector:
    matchLabels:
      app: tomcat
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1   
      maxUnavailable: 1
  template:
    metadata:
      name: tomcat
      labels:
        app: tomcat
    spec:
      containers:
      - name: tomcat
        image: tomcat:8.5.69
        ports:
        - containerPort: 8080
