# CatOps DevSecOps Delivery Demo

CatOps is a small Go web service used to practice the delivery path from source code to container image to Kubernetes release. The app is intentionally simple so the repo can focus on DevOps/SRE fundamentals: CI, image publishing, Helm packaging, Argo CD deployment, and platform bootstrap experiments.

## Project Status

This is a curated, public-safe portfolio snapshot. Hostnames, inventory entries, Vault tokens, and cluster-specific values have been replaced with examples. The repo is not meant to be applied directly to a production cluster without replacing the example configuration.

## Delivery Flow

```text
Go app
  |
  | GitHub Actions
  v
Docker image
  |
  | Helm values image tag update
  v
Helm chart
  |
  | Argo CD Application
  v
Kubernetes cluster
```

## What This Shows

- A containerized Go application with a minimal Dockerfile.
- GitHub Actions that builds and pushes an image, then updates the Helm chart tag.
- Dependabot coverage for GitHub Actions, Go modules, and Docker.
- A Helm chart with service, deployment, ingress, probes, and autoscaling scaffolding.
- Argo CD application manifests for Kubernetes delivery.
- Early platform experiments with K3s, Vault, Cloudflare Tunnel, and network policies.

## Repository Layout

```text
app/                         Go service source
.github/workflows/           CI automation
.github/dependabot.yml       Dependency update automation
kubernetes/my-app-chart/     Helm chart for deploying CatOps
ansible/                     K3s bootstrap experiments
ansible-argocd/              Argo CD and Vault bootstrap experiments
*.yaml                       Supporting Kubernetes manifests
```

## Security Notes

- CI reads Docker Hub credentials from GitHub Actions secrets.
- The Vault manifest runs dev mode for lab use only and does not pin a public root token.
- Argo CD initial passwords are not printed by the playbooks.
- Public hostnames and inventory values are examples, not live lab endpoints.

## Lessons Learned

- A tiny app is enough to practice the whole delivery chain.
- CI that mutates deployment manifests is useful for learning, but GitOps image automation or digest pinning would be cleaner for production.
- Platform bootstrap code should avoid printing credentials, even in a lab.
- Separating app delivery from cluster platform configuration makes the repo easier to review.

## Learning Timeline

- Started with a Go app and Docker image.
- Added GitHub Actions for build and publish automation.
- Wrapped deployment in Helm.
- Connected the chart to Argo CD.
- Experimented with Vault, Cloudflare Tunnel, and K3s bootstrap patterns.
