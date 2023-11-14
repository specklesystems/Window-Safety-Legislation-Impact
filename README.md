[![build and deploy Speckle functions](https://github.com/specklesystems/speckle-automate-code-compliance-window-safety/actions/workflows/main.yml/badge.svg)](https://github.com/specklesystems/speckle-automate-code-compliance-window-safety/actions/workflows/main.yml)

# Speckle Automate Function: Window Safety Legislation Impact Demo

## Overview
The "Window Safety Legislation Impact" function in Speckle Automate is a demonstration tool designed for the AEC industry. It allows users to assess if their building models comply with upcoming safety legislation regarding window sill heights.

## ⚠️ Disclaimer: Conceptual Demonstration Only
**IMPORTANT: This function is a conceptual demonstration and is not intended for production use. It aims to showcase how Speckle Automate can be used to assess compliance with specific safety standards in building designs.**

## Functionality
- **Legislation Compliance Check:** Analyzes window designs in AEC models against the new safety legislation requirements.
- **Automated Impact Assessment:** Automatically identifies windows that do not comply with the sill height requirements (either at threshold level or 0.85cm from the floor).
- **Reporting:** Generates reports highlighting non-compliant windows, aiding in planning for necessary modifications.

### How It Works
The function scans building models in Speckle for windows, measuring their sill heights and comparing them against the specified safety legislation standards.

### Potential Applications
- **Pre-emptive Compliance:** Helps architects and builders proactively adjust designs to meet new safety standards.
- **Safety Audits:** Assists in conducting safety audits of existing buildings for potential retrofitting.
- **Regulatory Reporting:** Supports creating compliance reports for regulatory submissions or internal reviews.

**Reminder:** This repository is for demonstration purposes, focusing on the impact of new window safety legislation in the AEC industry, and does not offer a practical implementation solution.

### Using this Speckle Function

1. [Create](https://automate.speckle.dev/) a new Speckle Automation.
1. Select your Speckle Project and Speckle Model.
1. Select the existing Speckle Function named [`Random comment on IFC beam`](https://automate.speckle.dev/functions/e110be8fad).
1. Enter a phrase to use in the comment.
1. Click `Create Automation`.

## Getting Started with creating your own Speckle Function

1. [Register](https://automate.speckle.dev/) your Function with [Speckle Automate](https://automate.speckle.dev/) and select the Python template.
1. A new repository will be created in your GitHub account.
1. Make changes to your Function in `main.py`. See below for the Developer Requirements, and instructions on how to test.
1. To create a new version of your Function, create a new [GitHub release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) in your repository.

## Developer Requirements

1. Install the following:
    - [Python 3](https://www.python.org/downloads/)
    - [Poetry](https://python-poetry.org/docs/#installing-with-the-official-installer)
1. Run `poetry shell && poetry install` to install the required Python packages.

## Building and Testing

The code can be tested locally by running `poetry run pytest`.

### Building and running the Docker Container Image

Running and testing your code on your own machine is a great way to develop your Function; the following instructions are a bit more in-depth and only required if you are having issues with your Function in GitHub Actions or on Speckle Automate.

#### Building the Docker Container Image

Your code is packaged by the GitHub Action into the format required by Speckle Automate. This is done by building a Docker Image, which is then run by Speckle Automate. You can attempt to build the Docker Image yourself to test the building process locally.

To build the Docker Container Image, you will need to have [Docker](https://docs.docker.com/get-docker/) installed.

Once you have Docker running on your local machine:

1. Open a terminal
1. Navigate to the directory in which you cloned this repository
1. Run the following command:

    ```bash
    docker build -f ./Dockerfile -t speckle_automate_python_example .
    ```

#### Running the Docker Container Image

Once the image has been built by the GitHub Action, it is sent to Speckle Automate. When Speckle Automate runs your Function as part of an Automation, it will run the Docker Container Image. You can test that your Docker Container Image runs correctly by running it locally.

1. To then run the Docker Container Image, run the following command:

    ```bash
    docker run --rm speckle_automate_python_example \
    python -u main.py run \
    '{"projectId": "1234", "modelId": "1234", "branchName": "myBranch", "versionId": "1234", "speckleServerUrl": "https://speckle.xyz", "automationId": "1234", "automationRevisionId": "1234", "automationRunId": "1234", "functionId": "1234", "functionName": "my function", "functionLogo": "base64EncodedPng"}' \
    '{}' \
    yourSpeckleServerAuthenticationToken
    ```

Let's explain this in more detail:

`docker run --rm speckle_automate_python_example` tells Docker to run the Docker Container Image that we built earlier. `speckle_automate_python_example` is the name of the Docker Container Image that we built earlier. The `--rm` flag tells docker to remove the container after it has finished running, this frees up space on your machine.

The line `python -u main.py run` is the command that is run inside the Docker Container Image. The rest of the command is the arguments that are passed to the command. The arguments are:

- `'{"projectId": "1234", "modelId": "1234", "branchName": "myBranch", "versionId": "1234", "speckleServerUrl": "https://speckle.xyz", "automationId": "1234", "automationRevisionId": "1234", "automationRunId": "1234", "functionId": "1234", "functionName": "my function", "functionLogo": "base64EncodedPng"}'` - the metadata that describes the automation and the function.
- `{}` - the input parameters for the function that the Automation creator is able to set. Here they are blank, but you can add your own parameters to test your function.
- `yourSpeckleServerAuthenticationToken` - the authentication token for the Speckle Server that the Automation can connect to. This is required to be able to interact with the Speckle Server, for example to get data from the Model.

## Resources

- [Learn](https://speckle.guide/dev/python.html) more about SpecklePy, and interacting with Speckle from Python.
