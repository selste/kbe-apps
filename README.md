# kbe-apps

Blog post: [ArgoCD Overview](https://kubebyexample.com/learning-paths/argo-cd/argo-cd-overview)

## Working with helm - Supplement

Changes wrt 'Accessing ArgoCD' in the 'ArgoCD Getting Started' section

- Patch the ArgoCD service from ClusterIP to a LoadBalancer instead of using port forwarding (From: [ArgoCD Tutorial](https://redhat-scholars.github.io/argocd-tutorial/argocd-tutorial/index.html))
  ```bash
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  ```

  Get the URL:
  ```bash
  argoURL=$(minikube service argocd-server -n argocd --url | tail -n 1 | sed -e 's|http://||')
  ```