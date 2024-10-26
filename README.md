# Continuous Deployment to Kubernetes Cluster using Helm

This project demonstrates a Continuous Integration and Continuous Deployment (CI/CD) pipeline for containerized applications, leveraging Jenkins, SonarQube, Docker, Helm, and Kubernetes. The pipeline includes automated code testing, static analysis, image building, and deployment to a Kubernetes cluster.

## Overview

The CI/CD pipeline, as illustrated in the diagram, automates the workflow from code commit to deployment on a Kubernetes cluster. Jenkins handles the CI/CD process, SonarQube performs static code analysis, and Helm manages the deployment to Kubernetes. Additionally, `kops` is used to create and manage the Kubernetes cluster, with a Jenkins slave node configured on a kops-managed VM for running Helm commands directly on the cluster.

![CICD for Containers](https://github.com/user-attachments/assets/7a6ecfe3-56a0-4e99-82d6-36329580ab9f)

## Pipeline Steps

1. **Code Commit**  
   The pipeline starts when a developer commits code changes to the GitHub repository.

2. **Code Fetching**  
   Jenkins fetches the latest code from GitHub, triggering the pipeline.

3. **Code Testing**  
   Jenkins runs automated tests to validate the functionality of the code.

   - **Pass**: The pipeline proceeds to the next step.
   - **Fail**: Notifications are sent, and the pipeline halts.

4. **Static Code Analysis**  
   Using SonarQube, the code undergoes a static analysis for quality checks.

   - **Pass**: The pipeline moves forward.
   - **Fail**: Notifications are sent, and the pipeline stops for code review.

5. **Image Building**  
   After successful analysis, Jenkins builds a Docker image for the application.

6. **Docker Image Push**  
   The built Docker image is pushed to Docker Hub for versioned storage and accessibility.

7. **Deployment using Helm**  
   The Docker image is then deployed to the Kubernetes cluster using Helm.

   - `kops` is used to create and manage the Kubernetes cluster.
   - A Jenkins slave node on a `kops` VM is configured to execute Helm commands directly on the Kubernetes cluster.

## Tools and Technologies

- **Jenkins**: Orchestrates the CI/CD pipeline and manages job execution.
- **SonarQube**: Performs static code analysis, ensuring code quality.
- **Docker**: Containers are created and managed using Docker.
- **Kubernetes**: The target environment for container deployment, managed by `kops`.
- **Helm**: Handles Kubernetes application deployment and management.
- **kops**: Creates and manages the Kubernetes cluster on the configured cloud provider.
  
## Prerequisites

1. **Jenkins Server**  
   - Install Jenkins and configure a pipeline job with necessary plugins (e.g., Git, SonarQube Scanner, Docker, and Kubernetes).

2. **SonarQube Server**  
   - Install and configure SonarQube for code quality analysis.

3. **Docker Hub**  
   - Docker repository to push and pull container images.

4. **Kubernetes Cluster**  
   - Set up a Kubernetes cluster using `kops`. Configure a VM as a Jenkins slave node for running Helm commands.

5. **Helm**  
   - Install Helm on the Jenkins slave node to deploy applications on Kubernetes.

## Pipeline Configuration

1. **Pipeline Script**: Define a Jenkinsfile in the project repository. This script includes stages for fetching code, testing, static analysis, building, and deploying the application.
   
2. **SonarQube Integration**: Configure Jenkins to send code analysis results to SonarQube and apply quality gates.

3. **Docker Hub Integration**: Set up credentials in Jenkins for pushing Docker images.

4. **Kubernetes and Helm Setup**  
   - Ensure `kops` and `kubectl` are configured to access the Kubernetes cluster.
   - Define Helm charts for deployment, specifying Kubernetes resources and configurations.

5. **Notifications**  
   - Configure email or messaging service integrations in Jenkins for notifications on pass/fail events.

## Running the Pipeline

To execute the pipeline:

1. **Commit Code**: Make a commit to the GitHub repository, triggering the Jenkins pipeline.
2. **Monitor Pipeline Stages**: Observe each stage in Jenkins, receiving notifications for pass/fail statuses.
3. **Deployment Verification**: After successful deployment, verify that the application is running on the Kubernetes cluster by checking pod status or accessing the application service.


## Conclusion

This CI/CD pipeline automates the deployment of containerized applications to Kubernetes, ensuring code quality and consistency across environments. The integration of Jenkins, SonarQube, Docker, Helm, and Kubernetes enables scalable and reliable application delivery.
