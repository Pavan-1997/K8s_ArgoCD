https://operatorhub.io/operator/argocd-operator


1. Install Operator Lifecycle Manager (OLM), a tool to help manage the Operators running on your cluster.
```
curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.24.0/install.sh | bash -s v0.24.0
```

2. Install the operator by running the following command:
```
kubectl create -f https://operatorhub.io/install/argocd-operator.yaml
```

3. To create pods for argo cd
   
Create a yml file : vi argo.yml
```
apiVersion: argoproj.io/v1alpha1
kind: ArgoCD
metadata:
  name: example-argocd
  labels:
    example: basic
spec: {}
```
```
kubectl create -f argo.yml
```

4. To access the UI 

kubectl edit svc example-argocd-server

change type fron ClusterIP to NodePort

5. To check the service

kubectl get svc

Access the UI from any of the nodes before that open the inbound rule


6. Creds for ArgoCD

Username: admin
Password:

kubectl get secret
(Argo CD stores the passwords in secrets)

kubectl edit secret example-argocd-cluster

(K8 secrets are base 64 encrypted not in plain text)

echo ZzNRZnlpbG9PWmgwdTJVTTVObUpIYjZMVENxc1J0YXY= | base64 -d

