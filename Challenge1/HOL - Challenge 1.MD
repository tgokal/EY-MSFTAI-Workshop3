# Welcome to Challenge 1


## <u> Aim </u>


In this Challenge, we will:

- Fork the Workshop GitHub repository and upload our training dataset to an Azure Machine Learning Compute Instance.

- Train and validate an insurance claim classification model.

- Verify that the model training process has been completed with the creation of a pkl file

!['Challenge 1 Architecture'](/Challenge1/images/challenge1architecture.PNG)

## <u> Steps </u>

As a team, complete the following tasks:


1. In your Azure subscription, create an Azure Machine Learning resource from the "Create a Resource" tile on the Homepage. 

    !['Create a Resource'](/Challenge1/images/challenge1_1.PNG)

    !['Create a Resource'](/Challenge1/images/challenge1_1a.PNG)

    Fill in the details to create an Azure Machine Learning workspace and other related resources.

    !['Fill out details for AML'](/Challenge1/images/challenge1_1b.PNG)

    - Keep Storage Replication as Locally-redundant storage (LRS)
    - You don't have to create a Container Registry
    - In the below table, see recommended names for resources.

        | Field         | Value    |
        |--------------|-----------|
        | `Subscription` | `<your subscription name>`      |
        | `Resource Group`      | `rg-Team-<your Team number>`  |
        | `Workspace name`      | `EY-Team-<your Team number>`  |
        | `Region`      | `australiaeast`  |
    
    - As you fill out your Azure ML Workspace name, the name for new Storage Account, Key vault and Application insight resources are created.

1. After creating your workspace in the Azure Portal, switch to the new Azure ML Studio so that we can use a web-based notebooks interface to work with it. 

    !['Launch Studio'](/Challenge1/images/challenge1_1c.PNG)

    !['Welcome to Studio'](/Challenge1/images/challenge1_1d.PNG)

1. To use Notebooks, create a `Standard_DS3_v2` Compute Instance from the Compute Tab and wait for it to start. 

    !['Create a Compute Instance'](/Challenge1/images/challenge1_1e.PNG)

1. Once the Compute Instance has been provisioned, open the Jupyter Lab environment link. 

    !['Open JupyterLab'](/Challenge1/images/challenge1_1f.PNG)
    !['Open JupyterLab'](/Challenge1/images/challenge1_1g.PNG)

1. Upload the Challenge files from this repo. This can be done manually or by using GitHub. 

    - If you're using GitHub, fork this repository. This will create a a clean template of all the necessary files for Challenges 1, 2 and 3 which you can change. Doing so leaves this original repository unchanged so that other Teams will see the same blank files.

    !['Fork this GitHub repo'](/Challenge1/images/challenge1_1h.PNG)

    - Start a new Terminal in your Jupyter Lab environment. 

    !['Create a new Terminal'](/Challenge1/images/challenge1_1ga.PNG)


    - Change directory into our Users folder using `cd` and `ls` from the Terminal. 
    - Clone your foked repo by typing the command `git clone <forked repo URL>` into the Terminal. 
    - You should see your files uploaded to your Jupyter environment within your Users folder.

    !['Loaded Files'](/Challenge1/images/challenge1_1i.PNG)

    - Click into the cloned files and navigate to Challenge 1.

1. Once your folders have been uploaded, navigate into the **Challenge 1** folder and upload the training data. You will find this CSV file in the Files tab within the Microsoft Teams site, called **porto_seguro_safe_driver_prediction_input.csv**

    !['Loaded Files'](/Challenge1/images/challenge1_1k.PNG)

1. In your Challenge 1 folder, open the **porto-seguro-safe-driver-prediction-LGBM.ipynb** notebook 

    !['Loaded Notebook'](/Challenge1/images/challenge1_1j.PNG)

1. Navigate to the **Kernel** in the top right hand corner of your Notebook and ensure that the kernel selected is **Python 3.6 - AzureML**

1. Run the code within each cell. 

    - You don't need to add code or change anything in this notebook. The code that is run will train and validate the insurance claim classification model. 

    - Verify that the model has been trained by viewing the model artefact, the trained model file - **.pkl**.

    !['Verify pkl file'](/Challenge1/images/challenge1_1l.PNG)


## <u> Coaching Questions </u>

Once you've completed the above steps, tag your Coach in your Team Channel and discuss the following Coaching questions with them:

1. What benefits and challenges can you see in using an Azure Machine Learning workspace as a central place for data scientisits and developers to collaborate on machine learning code?

2. What benefits and challenges can you see in using notebooks as a development interface for model training code - particularly in respect to automating training processes?


## <u> Success Criteria </u>  

To have completed this Challenge, you should have:  

- Provisioned an Azure Machine Learning workspace and at least 1 compute instance.

- Run the Challenge 1 notebook in your Azure Machine Learning compute instance and show your coach the training model *.pkl file

- Discuss Coaching Questions with your Coach and Team.