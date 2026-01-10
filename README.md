# Publi-Connect Infrastructure

This repository contains the Infrastructure-as-Code (IaC), CI/CD pipelines, and environment configurations for Publi-Connect-a captive portal system designed to manage internet access via Mikrotik routers.

## Repository Structure

*   `ci/`: GitHub Actions workflows and pipeline configurations.
*   `environments/`: Configuration for different deployment stages.
    *   `dev/`: Docker Compose and configuration for local development.
    *   `prod/`: AWS-specific configurations (Task Definitions, secrets, etc.).

## Development Environment Setup

We prioritize a Zero-Config developer experience. You do not need to manually manage Docker containers or databases.

### Prerequisites
*   Docker Desktop (Running)
*   Java 21+
*   Git

### Quick Start (Backend)

1.  **Prepare the Environment**
    Copy the development configuration files from `environments/dev/` in this repo to the root of your **backend application** repository:
    *   Copy `docker-compose.yml` -> `publi-connect-service-or-folder/compose.yaml`
    *   Copy `.env.example` -> `publi-connect-service-or-folder/.env`

2.  **Run the Application**
    Navigate to the backend repository and simply start the app:
    ```bash
    ./mvnw spring-boot:run
    ```

    **What happens automatically:**
    *   **Docker Compose** will automatically start the PostgreSQL database container.
    *   **Connection Details** are auto-injected into the application.
    *   **Environment Variables** are loaded from `.env`.
    *   **Hot Reload** is enabled for fast iteration.

3.  **Stop**
    When you stop the application (Ctrl+C), the database container will automatically shut down.

## Deployment

Deployment is handled via GitHub Actions located in the `ci/` directory.

*   **Production:** Deploys to AWS ECS (Fargate) upon pushing to the `main` branch.
*   **Infrastructure:** Uses AWS Secrets Manager for secure configuration management.
