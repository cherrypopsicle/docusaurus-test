---
sidebar_position: 1
---

# Getting Started

Hello and welcome to our Harbor documentation! It's a pleasure to know that you are joining the ride into our testing haven. Below you will find instructions to get kickstarted with our Harbor CLI.

## Harbor CLI

### Installing Harbor CLI

#### 1. Prerequisites Installation

Before we install the Harbor CLI, it's crucial that we have the following pre requisites:

- [AWS CLI](https://aws.amazon.com/cli/)
- [Docker](https://www.docker.com/products/docker-desktop/)

#### 2. Harbor CLI installation

**_NOTE: Before installing the Harbor CLI, make sure your Docker Daemon is running in the background_**

```brew
brew tap harbor-xyz/homebrew-harbor && brew install harbor
```

#### 3. Run Docker Desktop

### Configure your testnet

To create your Testnet, you'll need to configure harbor and create a config file. Use the command below to set up Harbor with the correct key and generate your first testnet config file. Once you enter the command, the CLI will guide you.

#### 1. Copy API Key

After logging in with your newly created Harbor account to the [Harbor WebApp](app.goharbor.com), you should be able to copy your API key in the top right corner where it says `API Key`.

#### 2. Create your config file

Run the command...

```bash
harbor configure
```

.. and follow along the CLI to create test configuration. If you want to bypass the configure command and just run a sample configuration, then here's one:

```json
{
  "config": {
    "name": "<testname>"
  },
  "chains": [
    {
      "chain": "ethereum",
      "config": {
        "artifactsPath": "./artifacts",
        "deploy": "./deploy",
        "environment": {
          "STAGE": "my-first-env-var"
        },
        "afterDeploy": {
          "location": "./afterDeploy"
        },
        "compiler": ""
      },
      "smartContracts": [
        {
          "fileName": "Greeter.sol",
          "name": "Greeter"
        },
        {
          "fileName": "Greeter2.sol",
          "name": "Greeter2"
        }
      ]
    },
    {
      "chain": "avalanche",
      "config": {
        "artifactsPath": "./artifacts",
        "deploy": "./deploy",
        "environment": {
          "STAGE": "connext-pre-release-avalanche"
        },
        "afterDeploy": {
          "location": "./afterDeploy"
        },
        "compiler": ""
      },
      "smartContracts": [
        {
          "fileName": "Greeter.sol",
          "name": "Greeter"
        },
        {
          "fileName": "Greeter2.sol",
          "name": "Greeter2"
        }
      ]
    },
    {
      "chain": "polygon",
      "config": {
        "artifactsPath": "./artifacts",
        "deploy": "./deploy",
        "environment": {
          "STAGE": "connext-pre-release-polygon"
        },
        "afterDeploy": {
          "location": "./afterDeploy"
        },
        "compiler": ""
      },
      "smartContracts": [
        {
          "fileName": "Greeter.sol",
          "name": "Greeter"
        },
        {
          "fileName": "Greeter2.sol",
          "name": "Greeter2"
        }
      ]
    }
  ],
  "offChainActors": [
    {
      "dockerfile": "./offChain/liquidation-bot-1/Dockerfile",
      "buildPath": "./offChain/liquidation-bot-1/",
      "name": "liquidation-bot-1",
      "port": 3000
    }
  ]
}
```

### Start your testnet

If you’ve successfully configured your JSON file, you should be able to start your first Testnet by setting up the infrastructure using the first command below and then starting the Testnet using the second command.

Make sure you are in the same directory as the config file!

#### 1. Create TestnetImage

```bash
// Note: Building testnet image might take a minute
harbor build
```

#### 2. Starting Testnet
After the TestnetImage has been successfully created, we can run that Testnet using the following command: 
```bash
harbor run <testnet_image_id> --name <unique_testnet_name>
```
