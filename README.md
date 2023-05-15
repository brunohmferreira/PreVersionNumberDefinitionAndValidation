# PreVersionNumberDefinitionAndValidation - Version Number: definition and validation

A series of sample Decorators for Azure Pipelines (Build).

Decorators in this repo work only with Azure DevOps (_they are not available in Azure DevOps Server_).

Check the [official documentation](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-pipeline-decorator) for more information about Azure Pipelines decorators.

## Intro to Decorators

It's an Azure Pipelines Decorator to define the version number and validates if downgrading or duplications are occurring

## About this repo structure

There are 2 types of Basic Decorators in this repo:

- __Build__: The Decorators in this folder work with ___both___ the Classic Build pipelines and the Multistage (_YAML_) pipelines. 
  - When running in YAML pipelines, they are applied to ___both___ __Jobs__ and __Deployment Jobs__
- __Release__: The Decorators in this folder work ___only___ with the Classic Release pipelines.

This project focus on a Build type and it runs after checkout in the pipeline.

## Getting Started

For __prerequisites__ take a look [here](https://docs.microsoft.com/en-us/azure/devops/extend/get-started/node?view=azure-devops#prerequisites)

### Build and Package the extension

First you need to install all the Node.js dependencies:

```cmd
npm install
```

Then you need to actually create the extension:

```cmd
tfx extension create
```

This will generate the _.vsix_ package file

### Publish the extension

When you have the extension file, head to [the marketplace management portal](https://marketplace.visualstudio.com/manage) and add the new extension.

You will also need to _share_ the extension to your organization.

> Only private extensions can contain Decorators, so be sure not to make it public.
For more info take a look at: https://docs.microsoft.com/en-us/azure/devops/extend/get-started/node?view=azure-devops#package-and-publish-your-extension

### Install the extension

Once shared with your Azure DevOps Organization, you can head to the _Manage Extensions_ tab under _Organization Settings_, go to _Shared_ and finally install your Decorato Extension.

For more info take a look at: https://docs.microsoft.com/en-us/azure/devops/extend/get-started/node?view=azure-devops#install-your-extension

### Use the extension

Once installed, you need to do the following steps to run the extension:
- Create a variable called "Decorator.VersionNumberDefinitionAndValidation.Enabled" and set it to _true_.
- Run the pipeline from a branch that has "/releases/" or "/hotfixes/" in the name.
- Configure pipeline to not run shallow fetch at checkout.
- Optional: create a variable "Version_Number_Format" to define the version number format. Default: "{0:d2}.{1:d3}.{2:d3}.{3}".
- Optional: create a variable "MajorNumber_max_delta" to define the maximum difference between the lastest and the next value of the major number considering the Semantic Versioning structure. Default: 0.
- Optional: create a variable "MinorNumber_max_delta" to define the maximum difference between the lastest and the next value of the minor number considering the Semantic Versioning structure. Default: 1.