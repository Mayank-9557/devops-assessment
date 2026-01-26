# devops-assessment
Implementation steps.

1.First, clone the project repository to your local machine.
2.Created a Dockerfile for the frontend
  Created a Dockerfile for the backend
3.Each Dockerfile uses multi-stage builds.
  Reduce image size
  Improve security
  Optimize build performance
4.Create docker-compose.yml
5.Build and Run Containers locally
  Run the command "docker compose up --build"
6.Set Up Self-Hosted GitHub Runner on a local machine
  Execute GitHub Actions workflows
  Allow Docker commands during CI/CD
  Enable local deployment automation
7.Created GitHub Actions Workflow
  .github/workflows/main.yml
  This Workflow: Triggers on every push to the main branch
                 Runs on the self-hosted runner
                 Automates build and deployment steps
8.Build and Push Docker Images to Docker Hub
  Logged in to Docker Hub
  Created repositories for:
      Frontend image
      Backend image

9.Added Docker Hub credentials to GitHub Secrets:
DOCKER_USERNAME
DOCKER_PASSWORD (or Access Token)
10.Updated GitHub Actions workflow

Log in to Docker Hub
Build Docker images
Tag images properly
Push images to Docker Hub automatically
11. Now, on every push to the main branch
     Images are built
     Images are pushed to Docker Hub automatically

CHALLENGE FACED DURING ASSESSMENT.
1.Issue:- After creating the Dockerfile and starting the application inside the container, the backend service failed to start due to a Gunicorn configuration error.
Incorrect module path
WSGI application loading failure

2.Root Cause
The issue occurred because
The Gunicorn command in the Dockerfile had an incorrect module reference.

To resolve the issue.
Debugged the container issue.
docker logs <container-name>
Verified the correct WSGI entry point for the Django application.
Rebuilt the image and restarted the containers.
After these fixes, the backend service started successfully and the application ran as expected.


