
# Desafío #10 - Instalación de ArgoCD en Minikube

## Requisitos
- Minikube
- kubectl
- Acceso a internet

## Pasos

### 1. Instalar kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```

### 2. Instalar ArgoCD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### 3. Obtener contraseña de acceso
```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```

### 4. Crear aplicación
```bash
kubectl apply -f manifests/app.yaml
```

## Evidencia
Ver carpeta `evidencias` para la captura del dashboard de ArgoCD.

## Estructura del Proyecto
```
proyecto-argocd/
├── docs/
│   └── README.md
├── manifests/
│   └── app.yaml
├── evidencias/
│   └── dashboard_argocd.png
```
