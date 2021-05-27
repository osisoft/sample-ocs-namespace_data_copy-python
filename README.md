# OSIsoft Cloud Services Namespace Migration Python Sample

**Version:** 1.0.0

[![Build Status](https://dev.azure.com/osieng/engineering/_apis/build/status/product-readiness/OCS/osisoft.sample-ocs-namespace_migration-python?repoName=osisoft%2Fsample-ocs-namespace_migration-python&branchName=main)](https://dev.azure.com/osieng/engineering/_build/latest?definitionId=3664&repoName=osisoft%2Fsample-ocs-namespace_migration-python&branchName=main)

Developed against Python 3.9.1.

## Requirements

- Python 3.9+
- Register a [Client-Credentials Client](https://cloud.osisoft.com/clients) in your OSIsoft Cloud Services tenant and create a client secret to use in the configuration of this sample. ([Video Walkthrough](https://www.youtube.com/watch?v=JPWy0ZX9niU))
- Install required modules: `pip install -r requirements.txt`

## About this sample

This sample uses REST API calls to copy dataviews, assets, and streams from a source namespace to a destination namespace. The steps are as follows

1. Copy the dataview specified by its Id and add all referenced assets and streams to lists to be copied later
1. Add all streams referenced by assets found by the specified query and referenced by the previously found dataview to a list to be copied later
1. Copy all streams found by the specified query and referenced by the previously found assets and dataview
1. Copy all assets found by the specified query and referenced by the previously found dataview
1. If testing, cleanup all created dataviews, assets, and streams

## Configuring the sample

The sample is configured using the file [config.placeholder.ini](config.placeholder.ini). Before editing, rename this file to `config.ini`. This repository's `.gitignore` rules should prevent the file from ever being checked in to any fork or branch, to ensure credentials are not compromised.

OSIsoft Cloud Services is secured by obtaining tokens from its identity endpoint. Client credentials clients provide a client application identifier and an associated secret (or key) that are authenticated against the token endpoint. You must replace the placeholders in your `config.ini` file with the authentication-related values from your tenant and a client-credentials client created in your OCS tenant. There are separate configurations for both the source and destination namespaces; however, there can be overlap in some settings such as TenantId, ClientId, ClientSecret, and even NamespaceId if, for example, you want to migrate to a namespace in the same tenant.

```ini
[SourceConfiguration]
NamespaceId = REPLACE_WITH_CURRENT_NAMESPACE_ID
TenantId = REPLACE_WITH_CURRENT_TENANT_ID
ClientId = REPLACE_WITH_CURRENT_CLIENT_ID
ClientSecret = REPLACE_WITH_CURRENT_CLIENT_SECRET
Resource = https://dat-b.osisoft.com
ApiVersion = v1

[DestinationConfiguration]
NamespaceId = REPLACE_WITH_NEW_NAMESPACE_ID
TenantId = REPLACE_WITH_NEW_TENANT_ID
ClientId = REPLACE_WITH_NEW_CLIENT_ID
ClientSecret = REPLACE_WITH_NEW_CLIENT_SECRET
Resource = https://dat-b.osisoft.com
ApiVersion = v1
```

## Running the sample

To run this example from the command line once the `config.ini` is configured, run

```shell
python program.py
```

## Running the automated test

To test the sample, run

```shell
pip install pytest
python -m pytest test.py
```

---

Tested against Python 3.9.1

For the main OCS samples page [ReadMe](https://github.com/osisoft/OSI-Samples-OCS)  
For the main OSIsoft samples page [ReadMe](https://github.com/osisoft/OSI-Samples)
