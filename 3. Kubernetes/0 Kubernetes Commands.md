# 🚀 Kubernetes: Popular & Useful Commands

This guide covers both **imperative** (CLI-based) and **declarative** (YAML-based) Kubernetes commands for managing resources efficiently.

---

## 📦 PODS

### ✅ Create
**Imperative:**
```bash
kubectl run nginx --image=nginx \
  --port=80 \
  --env="ENV=production" \
  --labels="app=nginx" \
  --restart=Never
```

**Declarative:**
```yaml
# pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```
```bash
kubectl apply -f pod.yaml
```

### 🔍 List & Describe
```bash
kubectl get pods
kubectl describe pod <pod-name>
```

### ❌ Delete
```bash
kubectl delete pod <pod-name>
kubectl delete -f pod.yaml
```

---

## 📂 DEPLOYMENTS

### ✅ Create
**Imperative:**
```bash
kubectl create deployment myapp --image=myapp:v1
```

**Declarative:**
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:v1
```
```bash
kubectl apply -f deployment.yaml
```

### 📌 Update Image
```bash
kubectl set image deployment/myapp myapp=myapp:v2
```

### 🔄 Rollout
```bash
kubectl rollout status deployment/myapp
kubectl rollout history deployment/myapp
kubectl rollout undo deployment/myapp
```

---

## 🛠️ SERVICES

### ✅ Create
**Imperative:**
```bash
kubectl expose deployment myapp --type=NodePort --port=80
```

**Declarative:**
```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 80
```
```bash
kubectl apply -f service.yaml
```

---

## 📚 CONFIGMAPS

### ✅ Create
**Imperative:**
```bash
kubectl create configmap my-config --from-literal=env=dev
```

**Declarative:**
```yaml
# configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  env: dev
```
```bash
kubectl apply -f configmap.yaml
```

### 🔍 View
```bash
kubectl get configmaps
kubectl describe configmap my-config
```

---

## 🔐 SECRETS

### ✅ Create
**Imperative:**
```bash
kubectl create secret generic my-secret --from-literal=password=123456
```

**Declarative:**
```yaml
# secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: MTIzNDU2 # base64 encoded
```
```bash
kubectl apply -f secret.yaml
```

---

## 🧠 NAMESPACES

```bash
kubectl create namespace dev
kubectl get namespaces
kubectl delete namespace dev
```

---

## 📊 RESOURCE UTILIZATION

```bash
kubectl top pod
kubectl top node
```

---

## ⚙️ APPLY / DELETE RESOURCES

```bash
kubectl apply -f <file>.yaml
kubectl delete -f <file>.yaml
```

---

## 📋 LOGS & EXEC

```bash
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash
```

---

## 🔄 PORT FORWARDING

```bash
kubectl port-forward pod/<pod-name> 8080:80
```

---

## 🧼 CLEANUP

```bash
kubectl delete all --all
kubectl delete pod,deployment,svc --all
```

---

## 🧪 DEBUGGING

```bash
kubectl get events
kubectl describe <resource> <name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- sh
```

---

## 🧰 OTHER USEFUL COMMANDS

```bash
kubectl version --short
kubectl config view
kubectl config current-context
kubectl get all
kubectl get nodes
```

---

## ✅ TIPS

- Use `-n <namespace>` to specify a namespace.
- Use `kubectl explain <resource>` for schema details.
- Use `kubectl diff -f file.yaml` to see what will change before applying.

---

🔗 For more, check the official documentation: https://kubernetes.io/docs/reference/kubectl/
---
# 🔧 Other Useful Options for \`kubectl run nginx --image=nginx\`

The basic command:

```bash
kubectl run nginx --image=nginx
```

can be extended with various options:

### 1. Run as a Pod (Without Creating a Deployment)
```bash
kubectl run nginx --image=nginx --restart=Never
```

### 2. Specify Ports
```bash
kubectl run nginx --image=nginx --port=80
```

### 3. Setting Environment Variables
```bash
kubectl run nginx --image=nginx --env="ENV=production" --env="DEBUG=false"
```

### 4. Dry Run and Output as YAML (Declarative)
```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

### 5. Specify Command & Arguments
```bash
kubectl run nginx --image=nginx --restart=Never --command -- /bin/bash -c "echo Hello Kubernetes"
```

### 6. Expose Port on Multiple Containers or Custom Labels
```bash
kubectl run nginx --image=nginx --port=80 --labels="app=nginx,env=dev"
```

These options give you flexibility in how you initiate and manage your pods using a simple \`kubectl run\` command.
