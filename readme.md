## This a test Hello World HTML page

This is used in the tutorial <a href="https://computingforgeeks.com/perform-git-clone-in-kubernetes-pod-deployment/" target="_blank">How To Perform Git clone in Kubernetes Pod deployment</a>

The Pod deployment yaml:

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php
  labels:
    tier: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: php
      tier: backend
  template:
    metadata:
      labels:
        app: php
        tier: backend
    spec:
      volumes:
      - name: code
        persistentVolumeClaim:
          claimName: code
      containers:
      - name: php
        image: php:7.4-fpm
        volumeMounts:
        - name: code
          mountPath: /code
      initContainers:
      - name: install
        image: alpine/git
        args:
        - clone
        - --single-branch
        - --
        - https://github.com/geoinca/html.git
        - /code
        volumeMounts:
        - name: code
          mountPath: /code

```