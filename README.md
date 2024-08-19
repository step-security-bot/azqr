[![build](https://github.com/Azure/azqr/actions/workflows/build.yaml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/build.yaml)
[![CodeQL](https://github.com/Azure/azqr/actions/workflows/codeql.yml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/codeql.yml)
[![Github All Releases](https://img.shields.io/github/downloads/Azure/azqr/total.svg)]()
[![codecov](https://codecov.io/gh/Azure/azqr/branch/main/graph/badge.svg?token=VReik9rs3l)](https://codecov.io/gh/Azure/azqr)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Percentage of issues still open")

# Azure Quick Review

[![Open in vscode.dev](https://img.shields.io/badge/Open%20in-vscode.dev-blue)](https://vscode.dev/github/Azure/azqr)

**Azure Quick Review (azqr)** is a powerful command-line interface (CLI) tool that specializes in analyzing Azure resources to ensure compliance with Azure's best practices and recommendations. Its main objective is to offer users a comprehensive overview of their Azure resources, allowing them to easily identify any non-compliant configurations or areas for improvement.

## Azure Quick Review Recommendations

**Azure Quick Review (azqr)** scans your resources with 2 types of recommendations:

* **Azure Resource Graph (ARG)** queries provided by the [Azure Proactive Resiliency Library v2 (APRL)](https://aka.ms/aprl) project.
* **Azure Resource Manager (ARM)** queries built  with the Golang SDK

To learn more about the recommendations used by **Azure Quick Review (azqr)**, you can refer to the documentation available [here](https://azure.github.io/azqr/docs/recommendations/).

## Scan Results

The output generated by **Azure Quick Review (azqr)** is written by default to an Excel file, which contains the following sheets:

* **Recommendations**: a list with all recommendations with the number of resources that are impacted. You can youse this table as an action plan to improve the compliance of your resources.
* **ImpactedResources**: a list with all resources that are impacted. You can use this table to identify resources that have issues that need to be addressed.
* **ResourceTypes**: a list of impacted resource types.
* **Inventory**: a list of all resources scanned by the tool. Here you'll find details such as SKU, Tier, Kind or calculated SLA. 
* **Advisor**: a list of recommendations provided by Azure Advisor.
* **Defender**: a list of Microsoft Defender for Cloud plans and their tiers.
* **Costs**: a list of costs associated with the scanned subscription for the last 3 months.

> By default, Azure Quick Review (azqr) obfuscates the Subscription Ids in the output to ensure the protection of sensitive information and maintain data privacy and security. If you want to display the Subscription Ids without obfuscation, you can use the `--mask=false` flag when executing the tool.

> Azure Quick Review can also generate an csv files with the same information as the excel. To generate the csv files, you can use the `--csv` flag when running the tool.

> A Power BI template is also available to help you visualize the results generated by Azure Quick Review. You can create the template running Azure Quick Review with the `pbi` command and then loading the excel file generated by the tool.

## Supported Azure Services

**Azure Quick Review (azqr)** currently supports the following Azure services:

* Microsoft.AVS/privateClouds
* Microsoft.AnalysisServices/servers
* Microsoft.ApiManagement/service
* Microsoft.App/containerApps
* Microsoft.App/managedenvironments
* Microsoft.AppConfiguration/configurationStores
* Microsoft.Automation/automationAccounts
* Microsoft.Batch/batchAccounts
* Microsoft.Cache/Redis
* Microsoft.Cdn/profiles
* Microsoft.CognitiveServices/accounts
* Microsoft.Compute/galleries
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Compute/virtualMachines
* Microsoft.ContainerInstance/containerGroups
* Microsoft.ContainerRegistry/registries
* Microsoft.ContainerService/managedClusters
* Microsoft.DBforMariaDB/servers
* Microsoft.DBforMariaDB/servers/databases
* Microsoft.DBforMySQL/flexibleServers
* Microsoft.DBforMySQL/servers
* Microsoft.DBforPostgreSQL/flexibleServers
* Microsoft.DBforPostgreSQL/servers
* Microsoft.Dashboard/grafana
* Microsoft.DataFactory/factories
* Microsoft.Databricks/workspaces
* Microsoft.DesktopVirtualization/hostPools
* Microsoft.DesktopVirtualization/scalingPlans
* Microsoft.DesktopVirtualization/workspaces
* Microsoft.Devices/IotHubs
* Microsoft.DocumentDB/databaseAccounts
* Microsoft.EventGrid/domains
* Microsoft.EventHub/namespaces
* Microsoft.Insights/activityLogAlerts
* Microsoft.Insights/components
* Microsoft.KeyVault/vaults
* Microsoft.Kusto/clusters
* Microsoft.Logic/workflows
* Microsoft.NetApp/netAppAccounts
* Microsoft.Network/ExpressRoutePorts
* Microsoft.Network/applicationGateways
* Microsoft.Network/azureFirewalls
* Microsoft.Network/connections
* Microsoft.Network/expressRouteCircuits
* Microsoft.Network/frontdoorWebApplicationFirewallPolicies
* Microsoft.Network/loadBalancers
* Microsoft.Network/natGateways
* Microsoft.Network/networkSecurityGroups
* Microsoft.Network/networkWatcherScanners
* Microsoft.Network/privateDnsZones
* Microsoft.Network/privateEndpoints
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/routeTables
* Microsoft.Network/trafficManagerProfiles
* Microsoft.Network/virtualNetworkGateways
* Microsoft.Network/virtualNetworks
* Microsoft.OperationalInsights/workspaces
* Microsoft.RecoveryServices/vaults
* Microsoft.ServiceBus/namespaces
* Microsoft.SignalRService/SignalR
* Microsoft.SignalRService/webPubSub
* Microsoft.Sql/servers
* Microsoft.Sql/servers/databases
* Microsoft.Sql/servers/elasticPools
* Microsoft.Storage/storageAccounts
* Microsoft.Synapse workspaces/bigDataPools
* Microsoft.Synapse/workspaces
* Microsoft.Synapse/workspaces/sqlPools
* Microsoft.VirtualMachineImages/imageTemplates
* Microsoft.Web/serverFarms
* Microsoft.Web/sites
* Specialized.Workload/AVD
* Specialized.Workload/AVS
* Specialized.Workload/HPC
* Specialized.Workload/SAP

## Usage

### Install on Linux or Azure Cloud Shell (Bash)

```bash
latest_azqr=$(curl -sL https://api.github.com/repos/Azure/azqr/releases/latest | jq -r ".tag_name" | cut -c1-)
wget https://github.com/Azure/azqr/releases/download/$latest_azqr/azqr-ubuntu-latest-amd64 -O azqr
chmod +x azqr
```

### Install on Windows

Use `winget`:

```console
winget install azqr
```

or download the executable file:

```
$latest_azqr=$(iwr https://api.github.com/repos/Azure/azqr/releases/latest).content | convertfrom-json | Select-Object -ExpandProperty tag_name
iwr https://github.com/Azure/azqr/releases/download/$latest_azqr/azqr-windows-latest-amd64.exe -OutFile azqr.exe
```

### Install on Mac

Download the latest release from [here](https://github.com/Azure/azqr/releases).

### Authentication

**Azure Quick Review (azqr)** supports the following authentication methods:

* Service Principal. You'll need to set the following environment variables:
  * AZURE_CLIENT_ID
  * AZURE_CLIENT_SECRET
  * AZURE_TENANT_ID
* Azure Managed Identity
* Azure CLI (Using this type of authentication will make scans run slower)

### Authorization

**Azure Quick Review (azqr)** requires the following permissions:

* Subscription Reader

### Running the Scan

To scan all resource groups in all subscription run:

```bash
./azqr scan
```

To scan all resource groups in a specific subscription run:

```bash
./azqr scan -s <subscription_id>
```

To scan a specific resource group in a specific subscription run:

```bash
./azqr scan -s <subscription_id> -g <resource_group_name>
```

For information on available commands and help run:

```bash
./azqr -h
```

### Excluding Recommendations and more

To prevent Azure Quick Review from scanning specific subscriptions, resource groups, services or recommendations, create a `yaml` file with the following format: 

```yaml
azqr:
  exclude:
    subscriptions:
      - <subscription_id> # format: <subscription_id>
    resourceGroups:
      - <resource_group_resource_id> # format: /subscriptions/<subscription_id>/resourceGroups/<resource_group_name>
    services:
      - <service_resource_id> # format: /subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/<service_provider>/<service_name>
    recommendations:
      - <recommendation_id> # format: <recommendation_id>
```

Then run the scan with the `--exclude` flag:

```bash
./azqr scan --exclude <path_to_yaml_file>
```

> Check the [rules](https://azure.github.io/azqr/docs/recommendations/) to get the recommendation ids.

## Troubleshooting

If you encounter any issue while using **Azure Quick Review (azqr)**, please set the `AZURE_SDK_GO_LOGGING` environment variable to `all`, run the tool with the `--debug` flag and then share the console output with us by filing a new [issue](https://github.com/Azure/azqr/issues).


## Support

This project uses GitHub Issues to track bugs and feature requests.
Before logging an issue please check our [troubleshooting](#troubleshooting) guide.

Please search the existing issues before filing new issues to avoid duplicates.

- For new issues, file your bug or feature request as a new [issue](https://github.com/Azure/azqr/issues).
- For help, discussion, and support questions about using this project, join or start a [discussion](https://github.com/Azure/azqr/discussions).

Support for this project / product is limited to the resources listed above.

## Contributors

Thanks to everyone who has contributed!

<a href="https://github.com/Azure/azqr/graphs/contributors">
  <img src="https://contributors-img.web.app/image?repo=Azure/azqr" />
</a>

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](CODE_OF_CONDUCT.md)

## Trademark Notice

> **Trademarks** This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow Microsoft’s Trademark & Brand Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to those third-party’s policies.
