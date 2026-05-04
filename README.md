


# Full-Stack Chat Application

This project is a full-stack chat application featuring a React-based frontend and a Node.js backend, enhanced with Kubernetes deployment and local CI/CD using Jenkins.

## Features

- Real-time messaging
- User authentication
- Responsive UI with Tailwind CSS
- Cloudinary integration for media uploads
- Socket.io for real-time communication

## Deployment and CI/CD

- **Kubernetes Integration**: The application is containerized and deployed on a local Kubernetes cluster using Kind.

- **Jenkins CI/CD**: Jenkins runs locally in a Docker container. Upon pushing code to GitHub, Jenkins automatically:
  - Pulls the latest code from GitHub.
  - Builds Docker images locally.
  - Pushes images to a local registry (registry2).
  - Deploys the updated application to the Kubernetes cluster.

### Setting up Jenkins Locally

To run Jenkins locally, execute the following Docker command:

```bash
docker run -d \
  --name jenkins \
  --restart=unless-stopped \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $HOME/.kube:/root/.kube \
  --network kind \
  jenkins/jenkins:lts
```

## Project Structure

- `backend/`: Node.js server with Express, MongoDB, and Socket.io
- `frontend/`: React application with Vite
- `k8s/`: Kubernetes manifests for deployment
- `Jenkinsfile`: Jenkins pipeline configuration

## Getting Started

1. Clone the repository
2. Set up the local Kubernetes cluster with Kind (see `kindConfig.sh`)
3. Deploy MongoDB and other services using the Kubernetes manifests
4. Run the Jenkins setup as above
5. Push changes to GitHub to trigger the CI/CD pipeline