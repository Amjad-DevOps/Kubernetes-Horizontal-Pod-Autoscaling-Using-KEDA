# Kubernetes-Horizontal-Pod-Autoscaling-Using-KEDA
Scale applications based on AWS SQS Queue using KEDA in Kubernetes

Prerequisite: Kubernetes Cluster

1. Install Keda in Kubernetes cluster
```
kubectl create namespace keda
helm repo add kedacore https://kedacore.github.io/charts
helm repo update

For EKS with Cilium:
helm install keda kedacore/keda --namespace keda --set metricsServer.dnsPolicy=ClusterFirstWithHostNet --set metricsServer.useHostNetwork=true

Others:
helm install keda kedacore/keda --namespace keda

Validation:
kubectl get pod -n keda

Logs:
kubectl logs -n keda {keda-pod-name}

```

2. Create a secret in Kubernetes using an IAM user's BASE64 encoded access and secret access keys.
```
kubectl apply -f kedaSecret.yaml
```

3. Create a Trigger Authentication
```
kubectl apply -f kedaTriggerAuth.yaml
```

4. Create KEDA Scaler (SQS) using the ScaledObject
```
kubectl apply -f kedaScaledObject.yaml
```

5. Validate 
```
kubectl get hpa -n keda

kubectl get scaledobject -n keda
```   
