# kbe-apps

Blog post: [ArgoCD Overview](https://kubebyexample.com/learning-paths/argo-cd/argo-cd-overview)

## Working with helm - Supplement

- Minikube
  ```bash
  minikube start --cpus "4" --memory "8g" --vm-driver=kvm2 --addons=ingress,metrics-server
  ```
- ArgoCD
  ```bash
  # Create namespace
  kubectl create namespace argocd
  # Install ArgoCD
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```

Changes wrt 'Accessing ArgoCD' in the 'ArgoCD Getting Started' section

- Patch the ArgoCD service from ClusterIP to a LoadBalancer instead of using port forwarding (From: [ArgoCD Tutorial](https://redhat-scholars.github.io/argocd-tutorial/argocd-tutorial/index.html))
  ```bash
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  ```
  
  Password:
  ```bash
  argoPassword=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
  ```

  URL:
  ```bash
  argoURL=$(minikube service argocd-server -n argocd --url | tail -n 1 | sed -e 's|http://||')
  ```

  CLI login:
  ```bash
  argocd login --insecure --username=admin --password=${argoPassword} ${argoURL}
  ```