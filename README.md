# OmniRAG DevOps

DevOps and CI/CD implementation for the OmniRAG project.

## Technologies

- Git and GitHub
- Docker and Docker Compose
- GitHub Actions
- GitHub Container Registry (GHCR)
- Kubernetes
- Google Cloud Platform (architecture evaluation)

## Repository Structure

- backend/: Backend Docker configuration
- frontend/: Frontend Docker configuration
- k8s/: Kubernetes manifests
- docs/: DevOps documentation
- .github/workflows/: CI/CD pipeline

## Application Source

The actual OmniRAG application is maintained separately:
https://github.com/Sananda-Dutta/Omnirag

## CI/CD Pipeline

GitHub Actions checks out the application repository, runs backend tests,
builds the frontend, and builds Docker images. Images are pushed to GHCR
on successful pushes to main.

## Kubernetes

The Kubernetes manifests provide a proposed deployment architecture.
They are not claimed to be deployed on a live cluster.
