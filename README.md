# Disable Replace Tokens Telemetry Transfer

# Context

The [Replace Tokens](https://marketplace.visualstudio.com/items?itemName=qetza.replacetokens) is a widely used Azure Devops Pipeline Extension to replace tokens in files. It offers the following benefits:
- Can be used by all pipelines requiring the replacement of tokens in files
- Supports all text formats beyond JSON and XML supported by built in File Transform pipeline task
- You don’t need to separately manage the variable values in config or parameter files. There is a direct relationship between a token and a corresponding variable.
- It supports secrets natively
- Is free

But it has one known con or risk. The Replace Tokens task for Azure Pipelines collects [anonymous usage data](https://github.com/qetza/vsts-replacetokens-task/issues/181) and sends them to its author to help improve the product.  If you don’t wish to send usage data, you can change your telemetry settings through **Send anonymous usage telemetry parameter**. For people who do not want to send any usage date, there is a risk to forget to unset the parameter **Send anonymous usage telemetry parameter** as it is set by default. 

To restrict the user to change the setting, the Replace Tokens offers a possibility to set the environment variable **REPLACETOKENS_DISABLE_TELEMETRY** and this will overwrite whatever the user can set/unset using **Send anonymous usage telemetry parameter**.

```typescript
  let telemetryEnabled = tl.getBoolInput('enableTelemetry', true) && tl.getVariable('REPLACETOKENS_DISABLE_TELEMETRY') !== 'true';
```

The current Azure Devops extension, which is a pipeline decorator, will set the **REPLACETOKENS_DISABLE_TELEMETRY** environment variable by injecting a step at the beginning of any pipeline execution.

# Installation

## Prerequisites

You must have the following permission and installations.

- You're an organization Owner.
- Install Node.js (we prefer [nvm](https://dev.to/skaytech/how-to-install-node-version-manager-nvm-for-windows-10-4nbi) package to be able to switch between different node.js versions). The version 12.0.0 was used to build the package.
- Install the extension packaging tool (TFX) by running npm install -g tfx-cli from a command prompt.

## Create a publisher

All extensions, including extensions from Microsoft, are under a publisher. Anyone can create a publisher and publish extensions under it. You can also give other people access to your publisher if a team is developing the extension.

1. Sign in to the Visual Studio [Marketplace management portal](https://aka.ms/vsmarketplace-manage).
2. If you don't already have a publisher, you'll be prompted to create one.
3. In the Create Publisher form, enter your name in the publisher name field. The ID field should get set automatically based on your name and can be adjusted

Make note of the ID. You need to set it in the manifest file of your extension.

## Package the extension

1. Clone the current github repository on your developement machine
2. Open your extension manifest file (vss-extension.json) and set the value of the publisher field to the ID of your publisher. For example:
```json
  {
    ...
    "id": "my-first-extension",
    "publisher": "PUT-THE-PUBLISHER-ID-HERE",
    ...
}
```
4. 

https://github.com/qetza/vsts-replacetokens-task/issues/181

# Use of Azure Pipelines Decorator to disable 

## All about Azure Pipelines Decorator

https://www.youtube.com/watch?v=1l-UAjdrSsM

## Steps to build Azure Pipelines Decorator Extension

https://docs.microsoft.com/en-us/azure/devops/extend/get-started/node?view=azure-devops#prerequisites


# References

- All you need to know about Azure Pipelines Decorators [Video](https://www.youtube.com/watch?v=1l-UAjdrSsM)
- [Disable Replace Tokens Telemetry transfer](https://github.com/qetza/vsts-replacetokens-task/issues/181)
- [Install Node.js using nvm on Windows 10](https://dev.to/skaytech/how-to-install-node-version-manager-nvm-for-windows-10-4nbi)




