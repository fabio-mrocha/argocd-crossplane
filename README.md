## K3S Installation
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" INSTALL_K3S_EXEC="--cluster-cidr=10.42.0.0/16 --service-cidr=10.43.0.0/16" sh -

## Creating argocd namespace
kubectl create namespace argocd

## Installing argocd using manifest
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## Installing argocd using manifest Helm chart
helm repo add argo https://argoproj.github.io/argo-helm
helm template argo-cd argo/argo-cd --version 7.6.2 --namespace argocd -f argocd-crossplane/argocd/gitops/values-argo-cd.yaml | kubectl -n argocd create -f -

## Find out argocd password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

## Accessing argocd via port-forward
kubectl port-forward -n argocd --address='0.0.0.0' service/argocd-server 8080:443

## In your browser, access ArgoCD 
https://localhost:8080
user: admin
pass:


## References
https://github.com/jonashackt/crossplane-argocd

https://cd.apps.argoproj.io/

https://docs.crossplane.io/latest/getting-started/provider-aws/