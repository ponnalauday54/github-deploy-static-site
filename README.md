#Static Website Hosting on Azure Storage with GitHub Actions

#Overview

This project demonstrates how to host a static website using Azure Storage and automate deployments using GitHub Actions.
Whenever code is pushed to the `main` branch, a CI/CD pipeline automatically uploads the latest files to Azure, ensuring the website is always up to date.


# Architecture

* Developer pushes code to GitHub
* GitHub Actions pipeline is triggered
* Pipeline authenticates with Azure
* Files are uploaded to `$web` container
* Website updates automatically

# Tech Stack

* GitHub Actions (CI/CD)
* Azure Storage (Static Website Hosting)
* Azure CLI
* HTML / CSS

# Features

* Static website hosting in Azure Blob Storage
* Automated deployment using GitHub Actions
* Secure authentication using Service Principal
* No manual deployment required
* Scalable and cost-effective hosting

#Project Structure

.
├── index.html
├── styles.css
└── .github/workflows/deploy.yml

# Run Locally

```bash
git clone <your-repo-url>
cd <your-project-folder>
open index.html
```

#Deployment Process

1. Code is pushed to the `main` branch
2. GitHub Actions pipeline runs automatically
3. Pipeline logs into Azure using secrets
4. Files are uploaded to `$web` container
5. Website is updated instantly


#GitHub Actions Workflow

```yaml
name: Deploy Static Website to Azure

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Login to Azure
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Upload files to Azure Storage
        run: |
          az storage blob upload-batch \
            --account-name ${{ secrets.STORAGE_ACCOUNT_NAME }} \
            --destination '$web' \
            --source . \
            --overwrite


#Security

* Credentials stored securely in GitHub Secrets
* No hardcoded passwords or keys
* Uses Azure Service Principal for authentication
