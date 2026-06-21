# Flask Restaurant Review App — Azure App Service Deployment

A Flask + PostgreSQL + Redis web app deployed to Azure App Service using a custom CI/CD pipeline built with GitHub Actions.

## What this project demonstrates

- Provisioning Azure resources (App Service, PostgreSQL Flexible Server, Azure Cache for Redis) manually via the Azure Portal
- Building a GitHub Actions workflow to automate deployment on every push to `main`
- Managing application configuration and secrets via App Service Environment Variables and GitHub Secrets
- Debugging real production startup failures using Azure's container logs (`az webapp log tail`)

## Architecture

GitHub (push to main)
→ GitHub Actions (build + deploy)
→ Azure App Service (Flask app, Python 3.12)
→ Azure Database for PostgreSQL (Flexible Server)
→ Azure Cache for Redis

## Base application

This project starts from Microsoft's official sample app ([Azure-Samples/msdocs-flask-postgresql-sample-app](https://github.com/Azure-Samples/msdocs-flask-postgresql-sample-app)). The application code (Flask routes, models, templates) is from this sample. Everything related to deployment — the GitHub Actions workflow, Azure resource configuration and environment variable setup was built independently.
