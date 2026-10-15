# Agile Assessment 9 – DevOps CI/CD Projects

This repository contains three independent CI/CD projects demonstrating automated DevOps pipelines using **GitHub → Jenkins → Docker → Kubernetes**.

---

## Repository Structure

```
agile_assessment9/
├── question1/          # Student Placement Portal
│   ├── index.html
│   ├── Dockerfile
│   ├── deployment.yaml
│   └── Jenkinsfile
├── question2/          # Online Bookstore
│   ├── index.html
│   ├── Dockerfile
│   ├── deployment.yaml
│   └── Jenkinsfile
└── question3/          # College Event Management Portal
    ├── index.html
    ├── Dockerfile
    ├── deployment.yaml
    └── Jenkinsfile
```

---

## Question 1 – Automated Student Placement Portal

**Features:** Student profiles, placement statistics, company profiles, recruitment drives, eligibility criteria.

**Stack:** HTML/CSS → Nginx Docker image → Kubernetes (2 replicas) → NodePort 30001

**CI/CD Stages:**
1. Clone Code
2. Build Docker Image
3. Smoke Test
4. Push to Docker Hub
5. Deploy to Kubernetes
6. Verify Pods

**Rollback:** Automatic via `kubectl rollout undo` in Jenkins `post { failure }` block.

---

## Question 2 – Online Bookstore with Automated Testing & Deployment Gates

**Features:** 9 books across 6 categories, search, shopping cart, order tracker, course rating summary (new feature).

**Stack:** HTML/CSS/JS → Nginx Docker image → Kubernetes (3 replicas) → NodePort 30002

**CI/CD Stages:**
1. Clone Code
2. Build Docker Image
3. Automated Smoke Test (deployment gate)
4. Security Scan Gate
5. Push to Docker Hub
6. Deploy to Kubernetes
7. Verify 3 Pods

**Rollback:** Automatic via `kubectl rollout undo` in Jenkins `post { failure }` block.

---

## Question 3 – College Event Management Portal with Rolling Updates

**Features:** 6 event types (hackathon, symposium, workshop, cultural, competition), schedule timeline, registration modal, status tracker, announcements (new company added).

**Stack:** HTML/CSS/JS → Nginx Docker image → Kubernetes (3 replicas) → NodePort 30003

**CI/CD Stages:**
1. Clone Code
2. Build Docker Image
3. Test Application
4. Push Image to Docker Hub
5. Deploy to Kubernetes (Rolling Update)
6. Verify 3 Pods Running

**Rollback:** Automatic via `kubectl rollout undo` in Jenkins `post { failure }` block.

---

## Jenkins Setup

### Credentials Required
| ID | Type | Purpose |
|---|---|---|
| `dockerhub-credentials` | Username & Password | Docker Hub login |
| `kubeconfig` | Secret File | Kubernetes cluster access |

### Before Running the Pipeline
Replace `YOUR_DOCKERHUB_USERNAME` in each `Jenkinsfile` and `deployment.yaml` with your actual Docker Hub username.

---

## Demonstrating Rollback

To simulate a faulty release:
1. Introduce a broken image tag or bad HTML in `index.html`
2. Push and trigger the pipeline
3. The smoke test will fail → Jenkins `post { failure }` triggers `kubectl rollout undo`
4. Verify the previous stable version is restored:
   ```bash
   kubectl rollout history deployment/<deployment-name>
   kubectl get pods -l app=<app-label>
   ```
