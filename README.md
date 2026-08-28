# GCP DevOps Project

A hands-on CI/CD project built on Google Cloud Platform, covering everything from sprint planning through a fully automated, multi-environment deployment pipeline to Google Kubernetes Engine (GKE).


## What This Project Demonstrates

- Agile project planning translated into infrastructure work
- Git-based workflows with branch protection and PR-gated deployments
- Containerized application delivery via Docker
- Automated CI/CD using Google Cloud Build
- Kubernetes deployment and service exposure on GKE
- Cluster cost and scaling optimization
- Isolated dev/prod environments with independent pipelines

## Sprint-by-Sprint Breakdown

**Sprint 1 — Source Control & Local Development**
- Created the GitHub repository and set it up per DevOps best practices
- Enabled branch protection on `main`, enforcing a PR-based workflow (feature branch → PR → review → merge) instead of direct pushes, to avoid merge conflicts
- Wrote and locally tested a simple containerized application (Docker)
- Pushed the working code to GitHub

**Sprint 2 — GCP & GKE Foundations**
- Created a GCP account and set up budget/billing alerts
- Studied Kubernetes fundamentals: automating deployment, scaling, and management of containers, plus core features like automated rollouts/rollbacks, self-healing, service discovery & load balancing, and security/config management
- Compared hosting options (own datacenter vs. AWS/Azure/GCP) and set up a GKE-managed cluster, using Node Auto-Provisioning and Cluster Autoscaler to optimize node/resource usage

**Sprint 3 — CI/CD Design**
- Ran a design discussion on how to automate the path from GitHub to GKE: build the Docker image automatically, store it in an artifact repository, write K8s deployment/service YAML, and set up continuous deployment to GKE
- Evaluated GCP-native tooling and selected **Cloud Build** (build automation) + **Google Container/Artifact Registry** (image storage) as the two core services

**Sprint 4 — Automating the Build (Cloud Build)**
- Connected the GitHub repository to Cloud Build
- Created a Cloud Build trigger so that any push to `main`/`master` automatically fires a build
- Defined the CI steps in `cloudbuild.yaml` (a fully serverless, YAML-defined pipeline with no infrastructure to manage)
- End-to-end flow at this stage: commit → open PR → merge to main → Cloud Build triggers → image built and pushed to Artifact Registry

**Sprint 5 — Deploying to GKE**
- Created a dedicated namespace in the GKE cluster (not `default`)
- Wrote the Kubernetes deployment file
- Updated `cloudbuild.yaml` so Cloud Build also handles deployment to GKE, not just the image build
- Validated the deployment end-to-end

**Sprint 6 — Exposing the Application**
- Extended the GKE deployment YAML to include a Service, exposing the application via an accessible endpoint

**Sprint 7 — Development Environment & Release Process**
- Stood up a separate development environment (its own branch and deployment path) alongside production
- Practiced promoting changes safely: develop → test in the dev environment → deploy to production following proper DevOps release flow
- Configured independent replica counts per environment to test scaling behavior separately from production

## Result

A fully automated CI/CD pipeline where a merged PR to GitHub triggers Cloud Build to build the Docker image, push it to Artifact Registry, and deploy it to the appropriate GKE namespace and endpoint — with an isolated development environment for safely testing changes before they reach production.

## Tech Stack

`GitHub` · `Docker` · `Google Cloud Build` · `Google Container/Artifact Registry` · `Google Kubernetes Engine (GKE)` · `Cloud IAM & Billing`
