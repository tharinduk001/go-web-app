# 🚀 Automated Web App Deployment with Kubernetes, Helm, GitHub Actions & ArgoCD

This project demonstrates a complete GitOps-driven CI/CD pipeline for deploying a containerized web application onto a Kubernetes cluster. It integrates Docker, Helm charts, GitHub Actions, and ArgoCD to enable fully automated builds, deployments, and environment synchronization.

---

## 📦 Tech Stack
- Kubernetes
- Docker
- Helm
- GitHub Actions
- ArgoCD
- GitHub Container Registry (GHCR)
- PowerShell / Bash
- Ingress / NodePort Services

---

## 🛠️ Pipeline Flow
### 1. Code Push → GitHub Actions
- Builds Docker image
- Tags with version + latest
- Pushes to GHCR

### 2. Helm Deployment
- Helm chart manages all Kubernetes resources
- Declarative config stored in repo

### 3. ArgoCD Sync
- Watches repo for changes
- Automatically deploys new version
- Ensures cluster matches Git state

### 4. Zero-Downtime Rollouts
- Kubernetes handles rolling updates safely

---

## 📁 Project Structure
```
├── .github/workflows/
│   └── ci-cd.yml
├── helm/
│   └── go-web-app/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│           ├── deployment.yaml
│           ├── service.yaml
│           └── ingress.yaml
├── Dockerfile
├── app/
│   └── (web application source code)
└── README.md
```

---

## 🚀 Deployment Steps
### 1. Clone Project
```bash
git clone https://github.com/<your-username>/<repo>.git
cd <repo>
```

### 2. Optional Local Build
```bash
docker build -t ghcr.io/<username>/go-web-app:latest .
```

### 3. Install Helm Chart
```bash
helm upgrade --install go-web-app ./helm/go-web-app -n default
```

### 4. Add to ArgoCD
```bash
argocd app create go-web-app \
  --repo https://github.com/<your-username>/<repo>.git \
  --path helm/go-web-app \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```

### 5. Sync
```bash
argocd app sync go-web-app
```

---

## 🌐 Accessing the Application
### NodePort
```
http://<node-ip>:<nodeport>
```

### Ingress
```
http://your-domain.com
```

---

## 🧪 Future Enhancements
- HPA (Autoscaling)
- Automated Helm version bumping
- Canary deployments via Argo Rollouts
- TLS with Cert-Manager
- Prometheus + Grafana Monitoring

---

## 📜 License
MIT License

---

## 🙌 Acknowledgements
Thanks to Kubernetes, Helm, ArgoCD, GitHub Actions, and Docker for powering this pipeline.
