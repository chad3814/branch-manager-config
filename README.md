# Branch Manager GitOps Configuration

GitOps configuration repository for the PostgreSQL Branch Manager service deployment.

## Repository Structure

```
branch-manager-config/
├── environments/
│   ├── production/
│   ├── staging/
│   └── development/
├── kubernetes/
│   ├── base/
│   └── overlays/
├── docker-compose/
├── argocd/
└── helm/
```

## Deployment Options

### Option 1: Docker Compose (Recommended for Start)
- **Pros**: Simple setup, easy debugging, minimal infrastructure
- **Cons**: Limited scalability, manual scaling
- **Best for**: Small teams, development, testing

### Option 2: Kubernetes on EC2
- **Pros**: Production-grade, auto-scaling, service discovery
- **Cons**: Complex setup, more maintenance overhead
- **Best for**: Production environments, multiple services

### Option 3: Hybrid Approach
- Start with Docker Compose
- Migrate critical services to K8s as you grow
- Use K8s for stateless services, Compose for stateful

## Quick Start

### Docker Compose Deployment
```bash
# Clone config repo
git clone https://github.com/chad3814/branch-manager-config.git
cd branch-manager-config

# Deploy production
cd docker-compose/production
docker-compose up -d

# Deploy staging
cd ../staging
docker-compose up -d
```

### Kubernetes Deployment
```bash
# Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Deploy applications
kubectl apply -f argocd/applications/
```

## Monitoring & Observability
- Prometheus + Grafana for metrics
- Loki for logs
- Jaeger for tracing (if needed)

## Security
- TLS termination at load balancer
- API key authentication
- Network policies (K8s) or network isolation (Docker)