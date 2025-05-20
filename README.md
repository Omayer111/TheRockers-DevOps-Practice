# TheRockers-DevOps-Practice

A sample Go application demonstrating modern DevOps practices with Kubernetes, Helm, CI/CD (GitHub Actions), and GitOps-based CD using Argo CD—all runnable locally with Docker Desktop.

---

## Features

- **Go Application**: Simple Go app with build and test support.
- **Kubernetes Manifests**: Deployments and services defined in YAML.
- **Helm Chart**: Parameterized Kubernetes resources for easy configuration and deployment.
- **CI/CD Pipeline**: Automated build, test, lint, Docker image build/push, and Helm chart update using GitHub Actions.
- **GitOps CD**: Automated deployment to Kubernetes using Argo CD.

---

## Project Structure

```
.
├── .github/workflows/ci.yaml      # GitHub Actions CI/CD pipeline
├── helm/                          # Helm chart for the application
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
├── k8s/manifests/                 # Raw Kubernetes manifests (for reference)
│   └── deployment.yaml
├── main.go                        # Go application source code
├── Dockerfile                     # Docker build instructions
└── README.md
```

---

## Getting Started

### 1. Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) with Kubernetes enabled
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)
- [Argo CD CLI (optional)](https://argo-cd.readthedocs.io/en/stable/cli_installation/)
- [Go](https://go.dev/doc/install) (for local development)

---

### 2. Build and Run Locally

```sh
go build -o myrock-app
./myrock-app
```

---

### 3. Deploy to Kubernetes with Helm

```sh
helm install myrock-app ./helm
```

To upgrade:
```sh
helm upgrade myrock-app ./helm
```

---

### 4. CI/CD Pipeline

- On every push to `main` (except changes to `README.md`, `helm/**`, or `k8s/**`), GitHub Actions will:
  - Build and test the Go app
  - Lint the code with `golangci-lint`
  - Build and push a Docker image to Docker Hub
  - Update the Helm chart with the new image tag and push the change

#### Example Workflow (`.github/workflows/ci.yaml`)

- **build**: Checks out code, sets up Go, builds, and tests.
- **code-quality**: Runs `golangci-lint`.
- **push**: Builds and pushes Docker image to Docker Hub.
- **update-newtag-in-helm-chart**: Updates the image tag in `helm/values.yaml` and commits the change.

---

### 5. Continuous Deployment with Argo CD

#### Install Argo CD

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

#### Access Argo CD UI

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Visit [https://localhost:8080](https://localhost:8080)
![image](https://github.com/user-attachments/assets/ee089876-9e6c-4d18-9fb5-8b1ee6882bc3)


#### Get Initial Admin Password (PowerShell)

```powershell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | %{ [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }
```

#### Create an Application in Argo CD

- **Repository URL**: Your GitHub repo
- **Revision**: `main`
- **Path**: `helm`
- **Cluster**: `https://kubernetes.default.svc`
- **Namespace**: `default`

Argo CD will now watch your repo and automatically deploy updates to your cluster.

---

## License

This project is for educational purposes.
inspired by Abhishek Veeramalla
