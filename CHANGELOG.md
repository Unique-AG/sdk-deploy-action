# `v3`
> [!CAUTION]
> 💥 `v3` is a breaking change as a new mandatory input `azure_storage_account_id` is introduced.

With v3 users are enabled to pass `azure_storage_account_id`, which under the hood reconfigures an environment to no longer use a Log Analytics Workspace but Azure Monitor instead. Using a [diagnostic setting](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings) the logs are sent to the specified storage account. From within Unique, users might then browse these logs using the `module` and `environment` names.

## 🔺 Upgrading from `v2`
`azure_storage_account_id` **must** now be supplied. 

Depending on wether your environment is provisioned by Unique or not, the value is injected into the repository via a variable and can be used like so:

```yaml
uses: Unique-AG/sdk-deploy-action@v3
with:
  azure_storage_account_id: ${{ vars.AZURE_STORAGE_ACCOUNT_ID }}
```