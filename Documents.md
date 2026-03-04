# Kubernetes-Based Full-Stack Application Deployment on AWS

## Overview
This project demonstrates an end-to-end DevOps implementation for deploying a
containerized full-stack application using Docker, Jenkins CI/CD, Kubernetes,
and Terraform on AWS.

## Architecture
- Jenkins for CI/CD automation
- Docker for containerization
- Kubernetes for orchestration
- Terraform for Infrastructure as Code
- AWS RDS for managed database
- VPC & Security Groups for secure networking

## CI/CD Workflow
1. Code pushed to GitHub
2. Jenkins pipeline triggered via webhook
3. Build frontend (NPM) and backend (Maven)
4. Build & push Docker images
5. Deploy to Kubernetes with rolling updates

## Kubernetes Deployment
- Deployments for frontend & backend
- Services (ClusterIP & LoadBalancer)
- Rolling updates with zero downtime
- Environment-based configuration

## Infrastructure as Code
- AWS VPC, Subnets, Security Groups
- RDS provisioning
- EKS / EC2-ready infrastructure
- Fully version-controlled using Terraform

## Key Features
- Zero-downtime deployments
- Secure AWS networking
- Scalable Kubernetes architecture
- Fully automated CI/CD

## Technologies
Docker, Kubernetes, Jenkins, Terraform, AWS RDS, VPC, Linux, Git, GitHub
