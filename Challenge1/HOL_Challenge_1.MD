# Welcome to Challenge 1

## <u> Business Problem and Use Case </u>

Underwriting is an essential part of car insurance through which insurers assess risk and determine premiums to accept it. Evaluating and pricing driver risk requires extensive research on the risk profile of the driver. Manual underwriting is time-consuming, prone to errors, and can lead to inefficient pricing. 

With many factors influencing whether or not a driver will submit a claim (i.e. age, health conditions, type of car, car mileage, previous driver record, etc.), there is a need for insurance companies to ensure that this process is accurate, timely, free of bias and can be automated. Predicting a correct claim amount has a significant impact on the strategy and operations of an insurer. 

Zooming out to an industry perspective:

- 56% of insurance executives believe that AI would improve operational efficiency. 
- 47% state that their investment in AI would accelerate over the next year.
- McKinsey estimates that 25% of the insurance industry will be automated in 2025 thanks to AI and machine learning techniques.

## <u> Technology Solutioning </u>

We will be creating a classification model in Azure Machine Learning that predicts whether a driver will submit an insurance claim, given factors about them, their vehicle, etc. 

The specific model that we'll be using is [LightGBM - a decision tree based algorithm developed by Microsoft](https://www.microsoft.com/en-us/research/project/lightgbm/). 

Just like how no man is an island, no model is an isolated system. For this model to provide a ROI and recurring value, it needs to be deployed to a compute resource so that business analysts at insurance firms can underwrite their customers accurately. 

Therefore, we'll be using [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/?nav=min) and the [MLOps Python repo](https://github.com/microsoft/MLOpsPython) to create a CICD pipeline and the infrastructure that comes with it to serve as the operating model in the insurance company.

## <u> Aim </u>


In Challenge 1, we will:

- Fork the Workshop GitHub repository and upload our training dataset *.csv file to the Jupyter Notebook environment running off a Compute Instance (VM)

- Train and validate an insurance claim classification model from a Jupyter Notebook *.ipynb.

- Verify that the model training process has been completed with the creation of a *.pkl file.

!['Challenge 1 Architecture'](/Challenge1/images/challenge1architecture.PNG)

## <u> Steps </u>

As a team, complete the following tasks:


1. In your Azure subscription, create an Azure Machine Learning resource from the "Create a Resource" tile on the Homepage. 

    !['Create a Resource'](/Challenge1/images/challenge1_1.PNG)

    !['Create a Resource'](/Challenge1/images/challenge1_1a.PNG)

    Fill in the details to create an Azure Machine Learning workspace and other related resources. You will need to create a new Resource Group. In the below table, see recommended names for resources.

    !['Fill out details for AML'](/Challenge1/images/challenge1_1b.PNG)

    | Field         | Value    |
    |--------------|-----------|
    | `Subscription` | `<your subscription name>`      |
    | `Resource Group`      | `rg-Team-<your Team number>`  |
    | `Workspace name`      | `EY-Team-<your Team number>`  |
    | `Region`      | `australiaeast`  |

    - Keep Storage Replication as Locally-redundant storage (LRS).
    - You don't have to create a Container Registry.
    - As you fill out your Azure ML Workspace name, the name for new Storage Account, Key vault and Application insight resources are created.
    - Click on the **Review + Create** and **Create** buttons to create the Azure Machine Learning resource and complementary resources.
    - Your deployment should be in progress.

    !['Deployment in progress'](/Challenge1/images/challenge1_1b1.png)

    - Once completed, click on the **Go to Resource** button.

    !['Deployment in progress'](/Challenge1/images/challenge1_1b2.png)

1. After creating your workspace in the Azure Portal, click on the **Launch Studio** button to switch to the new Azure ML Studio so that we can use a web-based notebooks interface to work with it. 

    !['Launch Studio'](/Challenge1/images/challenge1_1c.PNG)

    !['Welcome to Studio'](/Challenge1/images/challenge1_1d.PNG)

1. To use Notebooks, navigate to the Compute Tab and click on the **New** button.

    !['Welcome to Studio'](/Challenge1/images/challenge1_1d1.png)    

    Create a `Standard_DS3_v2` Compute Instance and name the instance `EYTeam{insert team number here}devbox`. The virtual machine type should be `CPU` and based in the location `australiaeast`. Further reading on what a [Compute Instance is in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-save-write-experiment-files).

    !['Create a Compute Instance'](/Challenge1/images/challenge1_1e.PNG)
    
    Click on the Next: Advanced Settings button to explore how you'd set up a virtual network in a prod environment, assign a compute to another user, etc. 
    
    **Don't change any of these settings - this is just for you to learn and expose yourself to the Advanced Settings.**

    !['Create a Compute Instance'](/Challenge1/images/challenge1_1e2.png)
    
    Click on the **Create** button to spin up your `Standard_DS3_v2` Compute Instance and wait for it to start. This should take 5-10 minutes.

    !['Open JupyterLab'](/Challenge1/images/challenge1_1f.PNG)

1. Once the Compute Instance has been provisioned, you should see this:

    !['Open JupyterLab'](/Challenge1/images/challenge1_1f1.png)


    Click on the Jupyter Lab environment link to be taken to an interactive Jupyter Lab environment where we can use Notebooks. 

    This is what you would see once the Jupyter Lab environment has loaded:

    !['Open JupyterLab'](/Challenge1/images/challenge1_1g.PNG)

    Navigate into the Users folder and into your subscription name folder, like so:

    !['Open JupyterLab'](/Challenge1/images/challenge1_1g1.png)

1. Upload the Challenge files from this repo. This can be done manually or by using GitHub. 

    - If you're using GitHub, fork this repository. This will create a a clean template of all the necessary files for Challenges 1, 2 and 3 which you can change. Doing so leaves this original repository unchanged so that other Teams will see the same blank files.

    !['Fork this GitHub repo'](/Challenge1/images/challenge1_1h.PNG)

    - Start a new Terminal in your Jupyter Lab environment. 

    !['Create a new Terminal'](/Challenge1/images/challenge1_1g.PNG)

    - Change directory into the Users folder using `cd` and `ls` from the Terminal. 

    !['Create a new Terminal'](/Challenge1/images/challenge1_1ga1.png)

    - Clone your foked repo here by typing the command `git clone <forked repo URL>` into the Terminal. 

    !['Create a new Terminal'](/Challenge1/images/challenge1_1gb.png)

    - You should see your files uploaded to your Jupyter environment within your Users/{subscription name} folder.

    !['Create a Resource'](/Challenge1/images/challenge1_1gd3.png)
    
    !['Create a Resource'](/Challenge1/images/challenge1_1gd2.png)

    - Click into the cloned files and navigate to Challenge 1.

    !['Create a new Terminal'](/Challenge1/images/challenge1_1gc1.png)

1. Once your folders have been uploaded, navigate into the **Challenge 1** folder. Create a **data** folder. 

    !['Create a new Terminal'](/Challenge1/images/challenge1_1gc.png)

    You will find the training data CSV file in the Files tab within the Microsoft Teams site, called **porto_seguro_safe_driver_prediction_input.csv**

    !['Loaded Files'](/Challenge1/images/challenge1_1k.PNG)

    

    Download the CSV file locally on your laptop and then upload the file into the **data** folder within Jupyter Lab. Click the **red Upload** button to confirm the upload. This upload will take 10-20 seconds.

    !['Create a new Terminal'](/Challenge1/images/challenge1_1gd.png)

    !['Loaded Files'](/Challenge1/images/challenge1_1gd1.png)

    !['Create a new Terminal'](/Challenge1/images/challenge1_1ge.png)

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

# On to Challenge 2
Click [here](https://github.com/tgokal/EY-MSFTAI-Workshop3/blob/master/Challenge23/HOL_Challenge_2.MD) to begin Challenge 2, where we will create Python Scripts for our model.