🚀 AI Task Platform Infrastructure
This repository manages the infrastructure and deployment manifests (Kubernetes) for the AI Task Platform. The project aims to provide a scalable, containerized environment for orchestrating and processing AI-driven tasks.

🏗️ Architecture Overview
The platform is composed of the following core components:

Frontend: A React/Next.js web application served via Nginx.

Backend: A Node.js/Express API that coordinates tasks and manages user data.

Worker: A Python-based service that handles resource-intensive AI processing from a Redis queue.

Databases:

MongoDB: Primary persistent data store for tasks, users, and results.

Redis: High-performance message broker and caching layer.

📂 Project Structure
Plaintext
ai-task-platform-infra/
├── k8s/
│   ├── 00-namespace.yaml      # Cluster isolation & logical grouping
│   ├── 01-configmap.yaml      # Non-sensitive environment variables
│   ├── 02-secret.yaml         # Sensitive data (DB credentials/API keys)
│   ├── 03-mongodb.yaml        # MongoDB Deployment & ClusterIP Service
│   ├── 04-redis.yaml          # Redis Deployment & ClusterIP Service
│   ├── 05-backend.yaml        # Backend API Deployment
│   ├── 06-worker.yaml         # AI Processing Worker Deployment
│   ├── 07-frontend.yaml       # Frontend Web UI Deployment & NodePort Service
│   └── ingress.yaml           # Ingress rules for external traffic routing
└── README.md
🛠️ Prerequisites
Ensure the following tools are installed before proceeding:

Docker Desktop (with Kubernetes enabled) or Minikube

kubectl (Kubernetes command-line tool)

Git

🚀 Deployment Steps
1. Clone the Repository
PowerShell
git clone https://github.com/anamparwez/ai-task-platform-infra.git
cd ai-task-platform-infra/k8s
2. Apply Infrastructure Manifests
Deploy all components in the correct sequence using the following command:

PowerShell
kubectl apply -f . -n ai-task-platform
3. Verify Deployment Status
Ensure all pods are in the Running state:

PowerShell
kubectl get pods -n ai-task-platform
🌐 Accessing the Application
Once successfully deployed, the services can be accessed via the following local ports:

Service	Protocol	Local Access
Frontend	HTTP	http://localhost:30080

Note: If you are using an Ingress Controller, ensure your local hosts file is configured to point to the defined domain.

🔧 Maintenance & Debugging
Cleanup non-running/stuck pods:

PowerShell
kubectl delete pods --field-selector status.phase!=Running -n ai-task-platform
Stream Backend logs:

PowerShell
kubectl logs -f deployment/backend -n ai-task-platform
Restart a specific deployment (e.g., Frontend):

PowerShell
kubectl rollout restart deployment frontend -n ai-task-platform
📝 Key Configuration
Environment variables are centralized in 01-configmap.yaml:

REDIS_HOST: Points to the internal redis service.

MONGODB_URI: Connection string for the internal mongodb service.

FRONTEND_URL: Configured to * for development to handle CORS.

Developed with ❤️ by Anam Parwez
