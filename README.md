# go-gin-sample-manifest
以下サンプルアプリのマニフェストコードリポジトリです。 \
https://github.com/1shikawa/go-gin-webapi

# Kustomize によるデプロイマニフェストの確認
```
▶ kustomize build ./overlays/dev
apiVersion: v1
kind: Service
metadata:
  name: sample
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: sample
  type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample
spec:
  replicas: 2
  revisionHistoryLimit: 3
  selector:
    matchLabels:
      app: sample
  template:
    metadata:
      labels:
        app: sample
    spec:
      containers:
      - image: 949993607219.dkr.ecr.ap-northeast-1.amazonaws.com/test-1shikawa:latest
        name: sample
        ports:
        - containerPort: 80
```

