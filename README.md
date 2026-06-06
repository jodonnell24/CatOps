# CatOps

CatOps is a small Go web app packaged for Kubernetes. The app serves a simple page and proxies cat images from the CATAAS API.

The repo includes the app source, Dockerfile, Helm chart, and an Argo CD `Application` manifest.

## Run Locally

```bash
cd app
go run .
```

The app listens on `PORT` when set, or `8080` by default.

## Build

```bash
docker build -t catops:local .
docker run --rm -p 8080:8080 catops:local
```

## Deploy

Render the Helm chart:

```bash
helm template catops charts/catops
```

Install it directly:

```bash
helm upgrade --install catops charts/catops
```

Or apply the Argo CD app manifest from a cluster that already has Argo CD installed:

```bash
kubectl apply -f argocd-app.yaml
```
