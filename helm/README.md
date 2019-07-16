# Setting up HELM

This document guides you on installing and configuring helm. You could also refer to the [Official Helm installation guide here](https://helm.sh/docs/using_helm/#installing-helm).

## Installing  Helm

To install helm you can follow following instructions.

```
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```

Verify the installtion is successful,
```
helm --help
```

Lets now setup  RBAC configurations required for Tiller, a component of helm that runs inside the kubernetes cluster.

`file: tiller-rbac.yaml`

```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```

You could also use `tiller-rbac.yaml` file which came along with this document.  Apply the RBAC policies required by tiller with,

```
kubectl apply -f tiller-rbac.yaml

```

This is where we actually initialize Tiller in our Kubernetes cluster.
```
helm init --service-account tiller
```

Validate by checking if tiller is running as part of your kubernetes environment,

```
kubectl get pods -n kube-system
```
