kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

kubectl port-forward -n argocd --address='0.0.0.0' service/argocd-server 8080:80

https://IP:8080
user: admin
pass:

https://github.com/jonashackt/crossplane-argocd

https://cd.apps.argoproj.io/

https://docs.crossplane.io/latest/getting-started/provider-aws/