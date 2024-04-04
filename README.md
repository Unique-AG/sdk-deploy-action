# Deploy Unique SDK Modules GitHub Action
This GitHub Action is designed to automate the deployment of Python modules developed with the Unique SDK to Azure Container Apps. It encapsulates the process of checking module requirements, setting up Azure CLI, logging into Azure Container Registry (ACR), building and pushing Docker images, and deploying the container app with specified scaling settings.

## Inputs
The action requires the following inputs:

* `module`: Name of the module to deploy. **(Required)**
* `environment`: Name of the environment to deploy the module to. **(Required)**
* `resourceGroupName`: Name of the resource group to deploy the module to. **(Required)**
* `acrLoginServer`: Azure Container Registry login server. **(Required)**
* `azureClientId`: Azure client ID. **(Required)**
* `azureTenantId`: Azure tenant ID. **(Required)**
* `azureSubscriptionId`: Azure subscription ID. **(Required)**
* `acrUsername`: Azure Container Registry username. **(Required)**
* `acrPassword`: Azure Container Registry password. **(Required)**
* `agePrivateKey`: Age private key. **(Required)**

The action also supports the following optional inputs:

* `app_name`: Name of the Flask app (and file). Default: `app`
* `encrypted_env_file`: Name of the encrypted environment file. Default: `.env.enc`
* `dockerfile`: Dockerfile for the container app. Default: `./Dockerfile`
* `sops_version`: Version of sops to use. Default: `3.8.1`
* `poetry_version`: Version of poetry to use. Default: `1.7.1`
* `min_replicas`: Minimum number of replicas for the container app. Default: `1`
* `max_replicas`: Maximum number of replicas for the container app. Default: `1`
* `location`: Location of the Azure Container Apps environment. Default: `switzerlandnorth`
* `cacheTag`: Tag to use for caching the docker build. Default: `dockercache`

## Outputs
The action provides the following outputs:

* `fqdn`: Fully Qualified Domain Name of the deployed Container App.
* `appName`: Name of the deployed Container App.
* `location`: Azure Location of the deployed Container App.
* `environment`: GitHub Environment of the deployed Container App.
* `resourceGroupName`: Azure Resource Group of the deployed Container App.

## Usage
To use this GitHub Action in your workflow, add the following step:

```yaml
- name: Deploy Unique SDK Module
  uses: Unique-AG/sdk-deploy-action@v1
  with:
    module: 'your-module-name'
    environment: 'your-environment-name'
    resourceGroupName: 'your-resource-group-name'
    acrLoginServer: 'your-acr-login-server'
    azureClientId: ${{ secrets.AZURE_CLIENT_ID }}
    azureTenantId: ${{ secrets.AZURE_TENANT_ID }}
    azureSubscriptionId: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
    acrUsername: ${{ secrets.ACR_USERNAME }}
    acrPassword: ${{ secrets.ACR_PASSWORD }}
    agePrivateKey: ${{ secrets.AGE_PRIVATE_KEY }}
    # Optional inputs can be omitted if defaults are suitable
```

Ensure you fill in the required inputs with your specific details.

## Prerequisites
Before using this action, ensure:

* You have an Azure account and have created an Azure Container Registry.
* The required secrets (AZURE_CLIENT_ID, AZURE_TENANT_ID, AZURE_SUBSCRIPTION_ID, ACR_USERNAME, ACR_PASSWORD, AGE_PRIVATE_KEY) are set in your GitHub repository.
* Your Python module follows the Unique SDK specifications and includes a pyproject.toml file with dependencies on gunicorn and python-dotenv.

This GitHub Action streamlines the deployment process, making it easier to deploy Unique SDK modules to Azure Container Apps with minimal setup.
