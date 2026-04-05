# 🚀 Kubernetes Ingress Lab – CKA Style

![Kubernetes](https://img.shields.io/badge/Kubernetes-CKA-blue?logo=kubernetes)
![Minikube](https://img.shields.io/badge/Minikube-Lab-orange)
![Ingress](https://img.shields.io/badge/Ingress-NGINX-green)
![Status](https://img.shields.io/badge/Project-Completed-success)

This project is a hands-on Kubernetes lab focused on mastering **Ingress configuration** using Minikube and the NGINX Ingress Controller.

The lab simulates real **CKA exam-level scenarios** including path routing, host routing, PathType rules, and default backend configuration.

---

## 📌 Lab Goals

* Enable Ingress Controller
* Deploy multiple backend services
* Configure Ingress rules
* Test routing with curl
* Understand Prefix vs Exact
* Use default backend
* Practice CKA-style troubleshooting

---

## 🧰 Technologies Used

* Kubernetes
* Minikube
* NGINX Ingress Controller
* YAML
* kubectl
* curl

---

![alt text](<ChatGPT Image Mar 15, 2026, 03_30_06 PM.png>)

## 📂 Project Structure

```
.
├── ingress-lab.yaml
└── README.md
```

All resources are inside **one manifest file**

✔ Deployments
✔ Services
✔ Ingress
✔ Routing rules
✔ Default backend

---

## ⚙️ Step 1 — Enable Ingress Controller

```bash
minikube addons enable ingress

kubectl get pods -n ingress-nginx

kubectl get ingressclass
```

---

## 📄 Step 2 — Apply Lab Manifest

```bash
kubectl apply -f ingress-lab.yaml
```

Check resources

```bash
kubectl get pods
kubectl get svc
kubectl get ingress
```

---

## 🌐 Routing Configuration

| Rule              | Destination     |
| ----------------- | --------------- |
| /                 | webapp-svc      |
| /api              | api-svc         |
| /admin            | admin-svc       |
| myapp.local       | webapp          |
| api.myapp.local   | api             |
| admin.myapp.local | admin           |
| unknown path      | default backend |

---

## 🔎 Get Ingress IP

```bash
kubectl get ingress
```

Example

```
NAME      CLASS   HOSTS        ADDRESS
ingress   nginx   myapp.local  192.168.67.2
```

---

## 🧪 Testing

### Path routing

```bash
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/api
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/admin
```

### Host routing

```bash
curl --resolve "api.myapp.local:80:192.168.67.2" http://api.myapp.local
curl --resolve "admin.myapp.local:80:192.168.67.2" http://admin.myapp.local
```

### Prefix vs Exact

```bash
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/api/users
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/admin
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/admin/settings
```

### Default backend

```bash
curl --resolve "myapp.local:80:192.168.67.2" http://myapp.local/anything
```

---

## 🧪 Lab Answers (Added)

### 🚀 Part 1

```
IngressClass name:
nginx

Why are the backend Services ClusterIP and not NodePort?
Because Ingress exposes services externally, so backend services remain internal (ClusterIP)
```

---

### 🔀 Part 2

```
ADDRESS:
192.168.49.2

Why does one Ingress replace 2 NodePort Services?
Because Ingress routes traffic to multiple services using a single entry point
```

---

### 🧠 Task 3

```
What response did /random return?
404 Not Found

How many rules does the routing table show?
3
```

---

### 🌐 Part 3

```
How many Host entries in describe output?
3

What happened with the unknown host?
404 Not Found

Difference between path-based and host-based routing:
Path-based: routing by URL path
Host-based: routing by domain name
```

---

### ⚙️ Task 5

```
Did /api/users work?
Yes

Did /admin/settings work? — why?
No
Because pathType Exact only matches /admin

When would you use pathType: Exact?
When strict matching is required
```

---

### 🔥 Task 6

```
Which service responded to /anything?
webapp-svc

Which service responded to http://myapp.local?
webapp-svc

Real-world use case for defaultBackend:
Fallback service for unmatched requests
```

---


## 🎯 What I Learned

✔ Ingress Controller setup
✔ Path-based routing
✔ Host-based routing
✔ Prefix vs Exact
✔ Default backend
✔ Single manifest deployment
✔ Real CKA troubleshooting

---

## 📊 Concepts Covered

* Ingress Controller
* ClusterIP Services
* Path Routing
* Host Routing
* PathType Prefix
* PathType Exact
* Default Backend
* NGINX Ingress

---

## 👨‍💻 Author

Abdelrahman El-Ashry
Junior DevOps Engineer

GitHub
https://github.com/elashrypublic

LinkedIn
https://www.linkedin.com/in/el-ashry

---

## ⭐ Support

If you like this project, give it a star ⭐
