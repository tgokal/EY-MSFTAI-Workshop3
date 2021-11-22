# Welcome to Challenge 4


## Aim

Your team now understands and has implemented the fundamentals concepts in a clocal development "execute from my notebook" experience and needs to apply all of these concepts to a production-ready workflow. 

A notebook is convenient for experimentation, but it's not suited for automating a full workflow. This is where Azure DevOps comes in. 

Using Azure DevOps Pipelines to operationalise Azure ML pipelines enables powerful tools such as version management, model/data validation, model evaluation/selection and stage deployments to QA/production. 

Your team will take the learnings and relevant Python scripts from the previous challenges and apply them to a new [MLOps Python](https://github.com/microsoft/MLOpsPython) code template to achieve these objectives. 

## Steps

- As a team carefully follow the [Getting Started guide](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md):

    - [Set up Azure DevOps](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#setting-up-azure-devops) to create an Azure DevOps organization.

    - Give your DevOps Organization a name and host the project in Australia East. Enter in the password characters and click **Continue**
    
         !['Challenge 2 Notebook'](/Challenge4/images/challenge4_g.png)

    - Enter your Project name to be `MCW-EY-DevOps-for-Data-Science` and choose the visibility to `Enterprise`.

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_h.png)

    - Install the [Azure Machine Learning extension by clicking on the link here](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#install-the-azure-machine-learning-extension). You'll arrive to the page like the screenshot below and click on the **Get it free** button.

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
    
- Once you've created the template in your GitHub account, **return back to your Terminal in your Jupyter Lab Environment on your Compute Instance**. 

    - In the Terminal, navigate to folder with your subscription name and clone your template using `git clone <url of your forked template>`. See how this is achieved in the screenshot below:
    
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_d.png)
     
    - Once it's been cloned, your directory will look like:
        
        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_n.png)

    - Navigate into the template directory and you will see the following:

        !['Challenge 2 Notebook'](/Challenge4/images/challenge4_e.png)

- Coming back to Azure DevOps, we now need to [create a variable group for the Pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#create-a-variable-group-for-your-pipeline). 

    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_s.png)
    !['Challenge 2 Notebook'](/Challenge4/images/challenge4_t.png)


    

- Next, we need to provision resources using Azure Pipelines with IaC (infrastructure as code) using this [link](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#provisioning-resources-using-azure-pipelines)

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

    - In your IaC provisioned Azure Machine Learning workspace, create a dataset in Azure Machine Learning using the same training data that you used from Microsoft Team and follow this section [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#configure-training-data).

    - If you have to make changes to a file within the `.pipelines/` folder, edit it from GitHub

    - Next, we need to update the scripts listed in the [Replace training code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-training-code) of the guide.

    - Update the [evaluation code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#update-evaluation-code), where you replace all instances of `mse` to `auc` and **disable the evaluation step** out of interest of time.

    - Once completed, create an Azure DevOps Pipeline and run a new build pipeline based on your `driver_training-ci.yml` pipeline definition in your forked repository. More details on what to do [here](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-model-ci-training-evaluation-and-registration-pipeline)

    - Rename this pipeline to `Model-Train-Register-CI`.

- Your first run of the build pipeline should **fail**. You will see many linting errors discovered. Attempt to resolve them in your scripts by looking at X for further details.

    - If you are short on time, comment out the linting test section in the `.pipelines/code-quality-template.yml` file.

- Once your build pipeline completes, you'll need to [replace the scoring code](https://github.com/microsoft/MLOpsPython/blob/master/docs/custom_model.md#replace-score-code). 

- Next, [set up the Release Deployment pipeline](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#set-up-the-release-deployment-pipeline)

    - Ignore the Batch Scoring pipeline - we won't be doing this today.

- Once the CD pipeline completes, you've finished Workshop 3. Congratulations!

- If you're keen to explore more, investigate what you'd need to change to [deploy to AKS or Azure App Service](https://github.com/microsoft/MLOpsPython/blob/master/docs/getting_started.md#further-exploration).