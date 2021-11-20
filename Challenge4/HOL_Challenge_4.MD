# Welcome to Challenge 4


## Aim

Your team now understands and has implemented the fundamentals concepts in a clocal development "execute from my notebook" experience and needs to apply all of these concepts to a production-ready workflow. 

A notebook is convenient for experimentation, but it's not suited for automating a full workflow. This is where Azure DevOps comes in. 

Using Azure DevOps Pipelines to operationalise Azure ML pipelines enables powerful tools such as version management, model/data validation, model evaluation/selection and stage deployments to QA/production. 

Your team will take the learnings and relevant Python scripts from the previous challenges and apply them to a new [MLOps Python](https://github.com/microsoft/MLOpsPython) code template to achieve these objectives. 

## Steps

- As a team carefully follow the [Getting Started guide](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md), where you will:

    - [Set up Azure DevOps](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#setting-up-azure-devops) to create an Azure DevOps organization and install the Azure Machine Learning extension. 

    - Create a template of the MLOps repo using the [repository template](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#get-the-code). Give your template a repository name.
    
    - Once you've created the template in your GitHub account, **open the compute instance using the VSCode button**. This will make it far easier to customize the template using VSCode. Open up a new terminal using `Ctrl + Shift + ~ `. Navigate outwards to a **different folder** and not in the `EY-MSFTAI-Workshop3` folder. This keeps the dev process separate from the CICD process.Clone the template once you're VSCode from the Terminal using `git clone <url of your forked template>`

    - Coming back to Azure DevOps, we now need to [create a variable group for the Pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#create-a-variable-group-for-your-pipeline). 

    - Next, we need to provision resources using Azure Pipelines with IaC (infrastructure as code) using this [link](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#provisioning-resources-using-azure-pipelines)

    - From the previous step, you would have created an Azure ML workspace. Now, we need to create a workspace service connection using this [link](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#create-an-azure-devops-service-connection-for-the-azure-ml-workspace).

- Switch over to the [Custom Model](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md) guide:

    - Firstly, we need to [bootstrap the directory structure of your cloned template repo files](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#bootstrap-the-project).

    - Create a dataset in Azure Machine Learning using the same training data that you used from Microsoft Team and follow this section [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#configure-training-data).

    - Next, we need to update the scripts listed in the [Replace training code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-training-code) of the guide.

    - Update the [evaluation code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#update-evaluation-code), where you replace all instances of `mse` to `auc` and **disable the evaluation step** out of interest of time.

    - Once completed, create an Azure DevOps Pipeline and run a new build pipeline based on your `driver_training-ci.yml` pipeline definition in your forked repository. More details on what to do [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-model-ci-training-evaluation-and-registration-pipeline)

    - Rename this pipeline to `Model-Train-Register-CI`.

- Your first run of the build pipeline should **fail**. You will see many linting errors discovered. Attempted to resolve them in your scripts by looking at X for further details.

    - If you are short on time, comment out the linting test section in the `.pipelines/code-quality-template.yml` file.

- Once your build pipeline completes, you'll need to [replace the scoring code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-score-code). 

- Next, [set up the Release Deployment pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-release-deployment-pipeline)

    - Ignore the Batch Scoring pipeline - we won't be doing this today.

- Once the CD pipeline completes, you've finished Workshop 3. Congratulations!

- If you're keen to explore more, investigate what you'd need to change to [deploy to AKS or Azure App Service](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#further-exploration).