apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep-home
  namespace: myapp
  labels:
    app: home
spec:
  replicas: 1
  selector:
    matchLabels:
      app: home
  template:
    metadata:
      labels:
        app: home
    spec:
      containers:
      - name: container-home
        image: srikanta1219/home:
        ports:
        - containerPort: 80

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep-jenkins
  namespace: myapp
  labels:
    app: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: container-jenkins
        image: srikanta1219/jenkins:
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep-docker
  namespace: myapp
  labels:
    app: docker
spec:
  replicas: 1
  selector:
    matchLabels:
      app: docker
  template:
    metadata:
      labels:
        app: docker
    spec:
      containers:
      - name: container-docker
        image: srikanta1219/docker:
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep-kubern8s
  namespace: myapp
  labels:
    app: kubern8s
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kubern8s
  template:
    metadata:
      labels:
        app: kubern8s
    spec:
      containers:
      - name: container-kubern8s
        image: srikanta1219/kubern8s:
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: home-svc
  namespace: myapp
  labels:
    app: home
spec:
  #type: LoadBalancer
  #type: NodePort
  ports:
  - port: 80
   #nodePort: 30001
  selector:
    app: home
---
apiVersion: v1
kind: Service
metadata:
  name: jenkins-svc
  namespace: myapp
  labels:
    app: jenkins
spec:
  #type: LoadBalancer
  #type: NodePort
  ports:
  - port: 80
   #nodePort: 30002
  selector:
    app: jenkins
---
apiVersion: v1
kind: Service
metadata:
  name: docker-svc
  namespace: myapp
  labels:
    app: docker
spec:
  #type: LoadBalancer
  #type: NodePort
  ports:
  - port: 80
   #nodePort: 30002
  selector:
    app: docker
---
apiVersion: v1
kind: Service
metadata:
  name: kubern8s-svc
  namespace: myapp
  labels:
    app: kubern8s
spec:
  #type: LoadBalancer
  #type: NodePort
  ports:
  - port: 80
   #nodePort: 30002
  selector:
    app: kubern8s
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: simple-micro-example
spec:
  rules:
  - host: micro.app.com
    http:
      paths:
      - path: /micro1
        pathType: Prefix
        backend:
          service:
            name: micro1-svc
            port:
              number: 30001
      - path: /micro2
        pathType: Prefix
        backend:
          service:
            name: micro2-svc
            port:
              number: 30002
      - path: /micro3
        pathType: Prefix
        backend:
          service:
            name: micro3-svc
            port:
              number: 30003
