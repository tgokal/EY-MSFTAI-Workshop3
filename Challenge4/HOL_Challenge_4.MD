# Welcome to Challenge 4


## Aim

Your team now understands and has implemented the fundamentals concepts in a clocal development "execute from my notebook" experience and needs to apply all of these concepts to a production-ready workflow. 

A notebook is convenient for experimentation, but it's not suited for automating a full workflow. This is where Azure DevOps comes in. 

Using Azure DevOps Pipelines to operationalise Azure ML pipelines enables powerful tools such as version management, model/data validation, model evaluation/selection and stage deployments to QA/production. 

Your team will take the learnings and relevant Python scripts from the previous challenges and apply them to a new [MLOps Python](https://github.com/microsoft/MLOpsPython) code template to achieve these objectives. 

# Setting up Azure DevOps

- As a team carefully refer to the [Getting Started guide](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md).

- Firstly, set up Azure DevOps to create an Azure DevOps organization.

    -  You'll use Azure DevOps for running the multi-stage pipeline with build, model training, and scoring service release stages. 
    - If you don't already have an Azure DevOps organization, create one by following the instructions at [Quickstart: Create an organization or project collection](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops). 
    - If you already have an Azure DevOps organization, create a new project using the guide at [Create a project in Azure DevOps and TFS](https://docs.microsoft.com/en-us/azure/devops/organizations/projects/create-project?view=azure-devops&tabs=preview-page). 

    - Give your DevOps Organization a name and host the project in Australia East. Enter in the password characters and click **Continue**
    
         !['Challenge 2 Notebook'](/Challenge4/images/challenge4_g.png)

    - Enter your Project name to be `MCW-EY-DevOps-for-Data-Science` and choose the visibility to `Enterprise`.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_h.png)

    - Install the [Azure Machine Learning extension by clicking on the link here](https://marketplace.visualstudio.com/items?itemName=ms-air-aiagility.vss-services-azureml). Install the Azure Machine Learning extension to your Azure DevOps organization from the Visual Studio Marketplace. This extension contains the Azure ML pipeline tasks and adds the ability to create Azure ML Workspace service connections. 
    
    - You'll arrive to the page like the screenshot below and click on the **Get it free** button.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_i.png)

        Select your Azure DevOps organisation that you've just created and **Install**.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_j.png)

        Once installed, you'll see the following:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_k.png)

        Click on **Proceed to Organization** to come back to the Azure DevOps organization. 
        
        Select your Project to be taken to the Project Overview page.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_l.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_m.png)

# Create MLOps Python Template
- Create a template of the MLOps repo using the [repository template](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#get-the-code). 

    - Navigate to the MLOps Python repo and click on the **Use this template** green button.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_a.png)

    - This will redirect you to the follow page - give your repository a name `EY_Team{team number}_MLOps` and set the visibility to `Public`. Click on the **Create repository from template** green button.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_b.png)

    - This will generate your template in your GitHub Account.
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_c.png)
    
- Once you've created the template in your GitHub account, **select the VSCode link to create a VSCode session from your Compute Instance**. 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode3.png)

    Select **Open**

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode4.png)

    You may be prompted to sign into your Azure subscription. Enter your details. 
    
    Select **Open again**, this will open up VSCode, like below:

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode5.png)

    Select **Select Yes Trust all authors**

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode6.png)

    In the Terminal, clone your MLOps template using `git clone <url of your forked template>` in a **different folder compared to your `EY-MSFTAI-Workshop3` repo.** 
    
    Please ensure this clone is in a different folder - it will save you an immense amount of confusion because we're delineating steps by keeping the directory folders separate.

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode1.png)

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode2.png)
# Create a Variable Group for your Pipeline
- Coming back to Azure DevOps, we now need to create a **variable group** for the Pipeline. MLOpsPython requires some variables to be set before you can run any pipelines. You'll need to create a variable group in Azure DevOps to store values that are reused across multiple pipelines or pipeline stages. Either store the values directly in  Azure DevOps or connect to an Azure Key Vault in your subscription. Check out the Add & use variable groups documentation to learn more about how to create a variable group and link it to your pipeline.

    Navigate to the **Library under the Pipelines tab** - you will see the following: 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_s.png)

    Create the following variable group called `devopsforai-aml-vg`. The YAML pipeline definitions in this repo refer to this variable group by this specific name. The variable group should contain the following required variables. Azure resources that don't exist yet will be created in the Provisioning resources using Azure Pipelines step below.

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_t.png)

    - Use `australiaeast` for `LOCATION`. We will need to add `australiaeast` as a valid `LOCATION` allowed value in the next step.
    - Change the name of your `BASE_NAME` variable to be `eyteam{your team number}`

- Some further information about these variables:

    - `BASE_NAME` is used as a prefix for naming Azure resources and should be unique. When sharing an Azure subscription, the prefix allows you to avoid naming collisions for resources that require unique names, for example, Azure Blob Storage and Registry DNS. Make sure to set `BASE_NAME` to a unique name so that created resources will have unique names, for example, MyUniqueMLamlcr, MyUniqueML-AML-KV, and so on. The length of the `BASE_NAME` value shouldn't exceed 10 characters and must contain letters and numbers only.
    - `LOCATION` is the name of the Azure location for your resources. There should be no spaces in the name. For example, `australiaeast`, `central`, `westus`, `westus2`.
    - `RESOURCE_GROUP` is used as the name for the resource group that will hold the Azure resources for the solution. If providing an existing Azure ML Workspace, set this value to the corresponding resource group name.
    
    - `WORKSPACE_NAME` is used for creating the Azure Machine Learning Workspace. You can provide an existing Azure ML Workspace here if you've got one.
    
    - `AZURE_RM_SVC_CONNECTION` is used by the Azure Pipeline in Azure DevOps that creates the Azure ML workspace and associated resources through Azure Resource Manager. You'll create the connection in a step below.
    
    - `WORKSPACE_SVC_CONNECTION` is used to reference a service connection for the Azure ML workspace. You'll create the connection after provisioning the workspace in the Create an Azure DevOps Service Connection for the Azure ML Workspace section below.
    
    - `ACI_DEPLOYMENT_NAME` is used for naming the scoring service during deployment to Azure Container Instances.
# Provisioning resources using Azure Pipelines
- Next, we need to provision resources using Azure Pipelines with IaC (infrastructure as code).

    - The easiest way to create all required Azure resources (Resource Group, Azure ML Workspace, Container Registry, and others) is to use the Infrastructure as Code (IaC) pipeline with ARM templates or the pipeline with Terraform templates. The pipeline takes care of setting up all required resources based on these Azure Resource Manager templates, or based on these Terraform templates.

    - Note: Since Azure Blob storage account required for batch scoring is optional, the resource provisioning pipelines mentioned above do not create this resource automatically, and manual creation is required before use.
    - Navigate to `environment_setup/arm-templates/cloud-environment.json` file in your forked MLOps Python repo. Add `"australiaeast"` as another entry in the `"allowed_values"` list. This gives us the choice to provide infrastructure in a region closer to home, saving costs. 

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_iac_change.png)

    - First create an Azure Resource Service Connection following the above link

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_u.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_v.png)

        Leave the `Resource Group` field empty.

        Note: Creating the Azure Resource Manager service connection scope requires 'Owner' or 'User Access Administrator' permissions on the subscription. You'll also need sufficient permissions to register an application with your Azure AD tenant, or you can get the ID and secret of a service principal from your Azure AD Administrator. That principal must have 'Contributor' permissions on the subscription.

        !['Challenge 2 Notebook'](/Challenge4/images/create-rm-service-connection.png)
# Create IaC Pipeline
- Once this is completed, you can create your Infrastructure as Code pipeline from your forked repository.

    !['Challenge 2 Notebook'](/Challenge4/images/build-connect.png)

    Select your MLOps Python repo template.

    !['Challenge 2 Notebook'](/Challenge4/images/select-a-repo.png)

    !['Challenge 2 Notebook'](/Challenge4/images/existing-azure-pipelines-yaml.png)

    Select the Existing Azure Pipelines YAML file option and set the path to `/environment_setup/iac-create-environment-pipeline-arm.yml` or to `/environment_setup/iac-create-environment-pipeline-tf.yml`, depending on if you want to deploy your infrastructure using ARM templates or Terraform:

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_w.png)

    Click **Run**

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_x.png)
    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_y.png)
    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_z.png)
    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_za.png)

    Once completed, you should see: 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_zb.png)

    Switching over to Azure, you'll see fully provisioned resources:
    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_zc.png)
    
# Create an Azure DevOps Service Connection for the Azure ML Workspace
- From the previous step, you would have created an Azure ML workspace. Now, we need to create a workspace service connection. Similar to the Azure Resource Manager service connection, you need to create an additional one for the Azure ML Workspace.

   -  Create a new service connection to your Azure ML Workspace using the Machine Learning Extension instructions to enable executing the Azure ML training pipeline. The connection name needs to match `WORKSPACE_SVC_CONNECTION` that you set in the variable group above (eg. 'aml-workspace-connection').

        !['Challenge 2 Notebook'](/Challenge4/images/ml-ws-svc-connection.png)

   - Note: Similar to the Azure Resource Manager service connection you created earlier, creating a service connection with Azure Machine Learning workspace scope requires 'Owner' or 'User Access Administrator' permissions on the Workspace. You'll need sufficient permissions to register an application with your Azure AD tenant, or you can get the ID and secret of a service principal from your Azure AD Administrator. That principal must have Contributor permissions on the Azure ML Workspace.
# Set up Model CI, training, evaluation and registration pipeline
- Switch over to the [Custom Model](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md) guide.
 ## Bootstrapping

- Firstly, we need to bootstrap the directory structure of your cloned template repo files.

    - Bootstrapping will prepare the directory structure to be used for your project name which includes:
        - Renaming files and folders from the base project name diabetes_regression to your project name 
        - Fixing imports and absolute path based on your project name
        - Deleting and cleaning up some directories
    - Note: Since the bootstrap script will rename the diabetes_regression folder to the project name of your choice, we'll refer to your project as [project name] when paths are involved.

- To bootstrap from the existing MLOpsPython repository:
    - Ensure Python 3 is installed locally
    - From a local copy of the code, run the bootstrap.py script in the bootstrap folder `python bootstrap.py -d dirpath -n projectname`
        - `dirpath` is the absolute path to the root of the directory where MLOpsPython is cloned
        - `projectname` is the name of your ML project. Ensure that you name the project `driver_training`. 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_aa.png)

## Register Dataset in Azure ML Workspace
- In your IaC provisioned Azure Machine Learning workspace, create a Tabular Dataset in Azure Machine Learning using the same training data that you used from Microsoft Team and follow this section [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#configure-training-data). If you code doesn't work, register it from the Azure ML UI.

    - Convert the template to use your own Azure ML Dataset for model training via these steps:
        - Create a Dataset in your Azure ML workspace
        - Update the `DATASET_NAME` and `DATASTORE_NAME` variables in `.pipelines/driver_training-variables-template.yml`
## Replace training code
- Next, we need to update the scripts listed in the below. The template contains three scripts in the `driver_training/training` folder. Update these scripts for your experiment code:
    - `train.py` contains the platform-agnostic logic required to do basic data preparation and train the model. This script can be invoked against a static data file for local development.
        - In your model code, remove the `early_stopping_rounds` parameter. It is used for dev purposes and will throw an warning in a prod environment within Azure DevOps.
    - `train_aml.py` is the entry script for the ML pipeline step. It invokes the functions in `train.py` in an Azure ML context and adds logging. `train_aml.py` loads parameters for training from `driver_training/parameters.json` and passes them to the training function in `train.py`. If your experiment code can be refactored to match the function signatures in `train.py`, this file shouldn't need many changes.
    - `test_train.py` contains tests that guard against functional regressions in `train.py`. Remove this file if you have no tests for your own code.
    - Add any dependencies required by training to `driver_training/conda_dependencies.yml`. This file will be used to generate the environment that the pipeline steps will run in.

    - Replace the contents of `driver_training/parameters.json` with the `parameters.json` file that we created in Challenge 2 like so:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_parametersjson.png)
    
    - Ensure that you're committing the changes to GitHub as you change each file `git status`, `git add <file>`, `git commit -m <message>` and `git push origin master`, or using the Source Control feature in VSCode like:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode7.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode8.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode9.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode10.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode11.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode12.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode13.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode14.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode15.png)

## Update evaluation code
- Update the evaluation code, where you replace all instances of `mse` to `auc` and **disable the evaluation step** out of interest of time. **Don't do Customize build agent environment section**

    - The MLOpsPython template uses the `evaluate_model` script to compare the performance of the newly trained model and the current production model based on Mean Squared Error. If the performance of the newly trained model is better than the current production model, then the pipelines continue. Otherwise, the pipelines are canceled.
    - To keep the evaluation step, replace all instances of mse in `driver_training/evaluate/evaluate_model.py` with the metric that you want.
    - To disable the evaluation step, either:
        - Set the DevOps pipeline variable `RUN_EVALUATION` to `false`
        - Uncomment `RUN_EVALUATION` in `.pipelines/driver_training-variables-template.yml` and set the value to `false`.
## Run Model CI Pipeline
- Once completed the **Update Evaluation Code** , create an Azure DevOps Pipeline and run a new build pipeline based on your `driver_training-ci.yml` pipeline definition in your forked repository. 

    - Now that you've provisioned all the required Azure resources and service connections, you can set up the pipelines for training (CI) and deploying (CD) your machine learning model to production. Additionally, you can set up a pipeline for batch scoring.

    - Model CI, training, evaluation, and registration - triggered on code changes to master branch on GitHub. 
        - Runs linting, unit tests, code coverage
        - Publishes and runs the training pipeline. 
        - If a new model is registered after evaluation, it creates a build artifact containing the JSON metadata of the model. 
        - Definition: `driver_training-ci.yml`.
    - Release deployment - consumes the artifact of the previous pipeline and deploys a model to either Azure Container Instances (ACI), Azure Kubernetes Service (AKS), or Azure App Service environments. 
        - Definition: `driver_training-cd.yml`.
        - Note: Edit the pipeline definition to remove unused stages. For example, if you're deploying to Azure Container Instances and Azure Kubernetes Service only, delete the unused Deploy_Webapp stage.

    - These pipelines use a Docker container on the Azure Pipelines agents to accomplish the pipeline steps. The container image `mcr.microsoft.com/mlops/python:latest` is built with this Dockerfile and has all the necessary dependencies installed for MLOpsPython template. 
    - This image is an example of a custom Docker image with a pre-baked environment. The environment is guaranteed to be the same on any building agent, VM, or local machine. 
    - In your project, you'll want to build your own Docker image that only contains the dependencies and tools required for your use case. Your image will probably be smaller and faster, and it will be maintained by your team.

- In your Azure DevOps project, create and run a new build pipeline based on the `driver_training-ci.yml` pipeline definition in your forked repository. If you plan to use the release deployment pipeline (in the next section), you will need to rename this pipeline to `Model-Train-Register-CI`.

- Your first run of the build pipeline should **fail**. You will see many linting errors discovered. Attempt to resolve them in your scripts by looking at the **Tests tab for your Pipeline run** for further details.

    - If you are short on time, comment out the linting test section in the `.pipelines/code-quality-template.yml` file.

    - You will need to install `lightgbm` using `pip` as an inline Python script within the `.pipelines/code-quality-template.yml` file.

    - A successful unit test and code coverage will look like:

        !['Challenge 2 Notebook'](/Challenge4/images/unit-tests.png)

        !['Challenge 2 Notebook'](/Challenge4/images/code-coverage-report.png)

- Once the pipeline is finished, check the execution result:

    !['Challenge 2 Notebook'](/Challenge4/images/model-train-register.png)

    !['Challenge 2 Notebook'](/Challenge4/images/model-train-register-artifacts.png)

- Also check the published training pipeline in the `mlops-AML-WS` workspace in Azure Machine Learning Studio:

    !['Challenge 2 Notebook'](/Challenge4/images/training-pipeline.png)

- Great, you now have the build pipeline for training set up which automatically triggers every time there's a change in the master branch!

- After the pipeline is finished, you'll see a new model in the ML Workspace:

    !['Challenge 2 Notebook'](/Challenge4/images/trained-model.png)

    - To disable the automatic trigger of the training pipeline, change the auto-trigger-training variable as listed in the `.pipelines\diabetes_regression-ci.yml` pipeline to false. You can also override the variable at runtime execution of the pipeline.
## Summary of Model CI Pipeline
- The pipeline stages are summarized below:
    - Model CI
        - Linting (code quality analysis)
        - Unit tests and code coverage analysis
        - Build and publish ML Training Pipeline in an ML Workspace
    - Train model
        - Determine the ID of the ML Training Pipeline published in the previous stage.
        - Trigger the ML Training Pipeline and waits for it to complete.
            - This is an agentless job. The CI pipeline can wait for ML pipeline completion for hours or even days without using agent resources.
        - Determine if a new model was registered by the ML Training Pipeline.
            - If the model evaluation determines that the new model doesn't perform any better than the previous one, the new model won't register and the ML Training Pipeline will be canceled. In this case, you'll see a message in the 'Train Model' job under the 'Determine if evaluation succeeded and new model is registered' step saying 'Model was not registered for this run.'
            - See evaluate_model.py for the evaluation logic.
            - Additional Variables and Configuration for configuring this and other behavior.
    - Create pipeline artifact
        - Get the info about the registered model
        - Create a pipeline artifact called model that contains a model.json file containing the model information.
# Set up the Release Deployment CD Pipeline

## Replace Score code
- Once your build pipeline completes, you'll need to **replace the scoring code**.

    - For the model to provide real-time inference capabilities, the score code needs to be replaced. The MLOpsPython template uses the score code to deploy the model to do real-time scoring on ACI, AKS, or Web apps.

    - If you want to keep scoring:

        - Update or replace `driver_training/scoring/score.py`
        - Add any dependencies required by scoring to `driver_training/conda_dependencies.yml`
        - Modify the test cases in the `ml_service/util/smoke_test_scoring_service.py` script to match the schema of the training features in your data.
        - Ensure that you replace the `test_row` in the `__main__()` function within `score.py` and the `input_data` dict in `smoke_test_scoring.py` with the our input data from the end of Challenge 3. This will run the data shaped for our features to the model when scoring occurs on the Azure Container Instance.

            -  Your data: [0,1,8,1,0,0,1,0,0,0,0,0,0,0,12,1,0,0,0.5,0.3,0.610327781,7,1,-1,0,-1,1,1,1,2,1,65,1,0.316227766,0.669556409,0.352136337,3.464101615,0.1,0.8,0.6,1,1,6,3,6,2,9,1,1,1,12,0,1,1,0,0,1],[4,2,5,1,0,0,0,0,1,0,0,0,0,0,5,1,0,0,0.9,0.5,0.771362431,4,1,-1,0,0,11,1,1,0,1,103,1,0.316227766,0.60632002,0.358329457,2.828427125,0.4,0.5,0.4,3,3,8,4,10,2,7,2,0,3,10,0,0,1,1,0,1]
            - **Keep the input_data on 1 line.**
## Deploy model to CD pipeline

- Next, set up the Release Deployment pipeline.

    - The release deployment and batch scoring pipelines have the following behaviors:
        - The pipeline will automatically trigger on completion of the `Model-Train-Register-CI` pipeline for the master branch.
        - The pipeline will default to using the latest successful build of the `Model-Train-Register-CI` pipeline. It will deploy the model produced by that build.
        - You can specify a `Model-Train-Register-CI` build ID when running the pipeline manually. You can find this in the url of the build, and the model registered from that build will also be tagged with the build ID. This is useful to skip model training and registration, and deploy/score a model successfully registered by a `Model-Train-Register-CI` build.

    - Ignore the Batch Scoring pipeline - we won't be doing this today.

    - In your Azure DevOps project, create and run a new build pipeline based on the diabetes_regression-cd.yml pipeline definition in your forked repository.

    - Your first run will use the latest model created by the Model-Train-Register-CI pipeline.

    - Once the pipeline is finished, check the execution result:

        !['Challenge 2 Notebook'](/Challenge4/images/model-deploy-result.png)

    - To specify a particular build's model, set the `Model Train CI Build Id` parameter to the build Id you would like to use:

        !['Challenge 2 Notebook'](/Challenge4/images/model-deploy-configure.png)

    - Once your pipeline run begins, you can see the model name and version downloaded from the `Model-Train-Register-CI` pipeline.

        !['Challenge 2 Notebook'](/Challenge4/images/model-deploy-get-artifact-logs.png)

- Deploy to ACI
    - Deploy the model to the QA environment in Azure Container Instances.
- Smoke test
    - The test sends a sample query to the scoring web service and verifies that it returns the expected response. 

 # Debugging Deployment
- If you encounter an error which prevents deployment, have a look at the Deployment logs for your Endpoint in your IaC provisioned Azure ML Workspace
- This will tell you what broke, what file it broke in and give you an error message that will assist you in understanding why it broke.

- Use this guide to [assist you in troubleshooting your model deployment](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-troubleshoot-deployment?tabs=azcli).

!['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode16.png)

# End of Workshop 4
- Once the CD pipeline completes, you've finished Workshop 3. Congratulations!

- If you're keen to explore more, investigate what you'd need to change to [deploy to AKS or Azure App Service](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#further-exploration).