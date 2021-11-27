# Welcome to Challenge 4


## Aim

Your team now understands and has implemented the fundamentals concepts in a clocal development "execute from my notebook" experience and needs to apply all of these concepts to a production-ready workflow. 

A notebook is convenient for experimentation, but it's not suited for automating a full workflow. This is where Azure DevOps comes in. 

Using Azure DevOps Pipelines to operationalise Azure ML pipelines enables powerful tools such as version management, model/data validation, model evaluation/selection and stage deployments to QA/production. 

Your team will take the learnings and relevant Python scripts from the previous challenges and apply them to a new [MLOps Python](https://github.com/microsoft/MLOpsPython) code template to achieve these objectives. 

## Steps

- As a team carefully follow the [Getting Started guide](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md):

    - [Set up Azure DevOps](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#setting-up-azure-devops) to create an Azure DevOps organization.

        -  You'll use Azure DevOps for running the multi-stage pipeline with build, model training, and scoring service release stages. 
         If you don't already have an Azure DevOps organization, create one by following the instructions at [Quickstart: Create an organization or project collection](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops). 
        - If you already have an Azure DevOps organization, create a new project using the guide at [Create a project in Azure DevOps and TFS](https://docs.microsoft.com/en-us/azure/devops/organizations/projects/create-project?view=azure-devops&tabs=preview-page). 

    - Give your DevOps Organization a name and host the project in Australia East. Enter in the password characters and click **Continue**
    
         !['Challenge 2 Notebook'](/Challenge4/images/challenge4_g.png)

    - Enter your Project name to be `MCW-EY-DevOps-for-Data-Science` and choose the visibility to `Enterprise`.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_h.png)

    - Install the [Azure Machine Learning extension by clicking on the link here](https://marketplace.visualstudio.com/items?itemName=ms-air-aiagility.vss-services-azureml). Install the Azure Machine Learning extension to your Azure DevOps organization from the Visual Studio Marketplace. This extension contains the Azure ML pipeline tasks and adds the ability to create Azure ML Workspace service connections. You'll arrive to the page like the screenshot below and click on the **Get it free** button.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_i.png)

        Select your Azure DevOps organisation that you've just created and **Install**.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_j.png)

        Once installed, you'll see the following:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_k.png)

        Click on **Proceed to Organization** to come back to the Azure DevOps organization. Select your Project to be taken to the Project Overview page.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_l.png)

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_m.png)

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

    Select **Open again**, this will open up VSCode, like below:

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode5.png)

    Select **Select Yes Trust all authors**

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode6.png)

    In the Terminal, clone your MLOps template using `git clone <url of your forked template>` in a different folder compared to your `EY-MSFTAI-Workshop3` repo.

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode1.png)

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode2.png)

- Coming back to Azure DevOps, we now need to [create a variable group for the Pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#create-a-variable-group-for-your-pipeline). 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_s.png)

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_t.png)

- Next, we need to provision resources using Azure Pipelines with IaC (infrastructure as code) using this [link](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#provisioning-resources-using-azure-pipelines).

    - Navigate to `environment_setup/arm-templates/cloud-environment.json` file in your forked MLOps Python repo. Add `"australiaeast"` as another entry in the `"allowed_values"` list. This gives us the choice to provide infrastructure in a region closer to home, saving costs. 

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_iac_change.png)

    - First create an Azure Resource Service Connection following the above link

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_u.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_v.png)

    - Once this is completed, you can create your Infrastructure as Code pipeline:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_w.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_x.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_y.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_z.png)
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_za.png)

        Once completed, you should see: 

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_zb.png)

        Switching over to Azure, you'll see fully provisioned resources:
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_zc.png)
    

- From the previous step, you would have created an Azure ML workspace. Now, we need to create a workspace service connection using this [link](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#create-an-azure-devops-service-connection-for-the-azure-ml-workspace).

- Switch over to the [Custom Model](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md) guide:

    - Firstly, we need to [bootstrap the directory structure of your cloned template repo files](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#bootstrap-the-project).

        - Ensure that you name the project `driver_training`. 

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_aa.png)

    - In your IaC provisioned Azure Machine Learning workspace, create a Tabular Dataset in Azure Machine Learning using the same training data that you used from Microsoft Team and follow this section [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#configure-training-data). If you code doesn't work, register it from the Azure ML UI.

    - Next, we need to update the scripts listed in the [Replace training code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-training-code) of the guide. 

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


    - Update the [evaluation code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#update-evaluation-code), where you replace all instances of `mse` to `auc` and **disable the evaluation step** out of interest of time. **Don't do Customize build agent environment section**

    - Once completed the **Update Evaluation Code** , create an Azure DevOps Pipeline and run a new build pipeline based on your `driver_training-ci.yml` pipeline definition in your forked repository. More details on what to do [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-model-ci-training-evaluation-and-registration-pipeline)

    - Rename this pipeline to `Model-Train-Register-CI`.

- Your first run of the build pipeline should **fail**. You will see many linting errors discovered. Attempt to resolve them in your scripts by looking at X for further details.

    - If you are short on time, comment out the linting test section in the `.pipelines/code-quality-template.yml` file.

    - You will need to install `lightgbm` using `pip` as an inline Python script within the `.pipelines/code-quality-template.yml` file.

- Once your build pipeline completes, you'll need to [replace the scoring code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-score-code). Ensure that you replace the `test_row` in the `__main__()` function within `score.py` and the `input_data` in `smoke_test_scoring.py` with the our input data from the end of Challenge 3. This will run the data shaped for our features to the model when scoring occurs on the Azure Container Instance. 

- Next, [set up the Release Deployment pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-release-deployment-pipeline)

    - Ignore the Batch Scoring pipeline - we won't be doing this today.
    - If you encounter an error which prevents deployment, have a look at the Deployment logs for your Endpoint in your IaC provisioned Azure ML Workspace:

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_vscode16.png)

- Once the CD pipeline completes, you've finished Workshop 3. Congratulations!

- If you're keen to explore more, investigate what you'd need to change to [deploy to AKS or Azure App Service](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#further-exploration).