#### Commands

```bash
# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password

```
</br>

#### Links



1️⃣ Create "test-argo-application":
Go to Argo CD UI → NEW APP

Fill in the fields based on:

Name: test-argo-application

Repo URL: https://github.com/ABHISHEK-KUMAR-14022001/argocd-app-config.git

Path: test

Cluster: https://kubernetes.default.svc

Namespace: myapp

Click "Create"

2️⃣ Create "kyverno-policies":
Repeat the above process, changing:

Name: kyverno-policies

Path: policy

Cluster: https://130.211.194.118

Namespace: kyverno

3️⃣ Create "prod-app":
Repeat again with:

Name: prod-app

Path: prod

Cluster: https://130.211.194.118

Namespace: deployapp

* Config repo: [https://gitlab.com/nanuchi/argocd-app-config](https://gitlab.com/nanuchi/argocd-app-config)

* Docker repo: [https://hub.docker.com/repository/docker/nanajanashia/argocd-app](https://hub.docker.com/repository/docker/nanajanashia/argocd-app)

* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)





Explanation:

automated: selfHeal: true → Ensures ArgoCD will monitor changes and sync automatically.
retry: limit: 3 → If a sync fails, it will retry 3 times.
backoff: duration: 5m → Argo CD will retry syncing every 5 minutes.
factor: 2 → The backoff interval will increase exponentially.
maxDuration: 30m → Ensures retrying does not go beyond 30 minutes.
