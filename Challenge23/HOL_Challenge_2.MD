# Welcome to Challenge 2

Here, we'll continue our work from Challenge 1.

To recap, in Challenge 1, we created an Azure ML workspace and registered a PKL file for the LightGBM classification model that we'll use to predict whether a driver submits an insurance claim or not. Doing so will save time, scope and cost for a Customer as we're not only automating a lengthy business process but also predicting a quantity that provides immense value to underwriting by considering latent variables and the distribution of those variables as well as the intrinsic relationships between the features and the targets.

In Challenge 2, we'll continue our journey of MLOps by evolving our code in the Jupter Notebook to a Python Script. This is typically done so that we're able to package our ML model into a software image that can be rebuilt on a container or some type of compute in a Customer, orchestrated by a CICD pipeline. 


## <u> Aim </u>


Specifically, we will:

- Create a training script called `train.py` using the code from Challenge 1 and our `*.csv` training data.

- Perform unit tests and linting tests on the training script to ensure that it meets the PEP8 software engineering standard.

- Train our machine learning model on a Compute Instance (VM) by creating an Experiment in Azure ML using the ScriptRunConfig() object. This object allows us to submit our own model script - like our `train.py` - as part of a training experiment pipeline. In practice, we can use the ScriptRunConfig() object to train any custom model in Azure ML. The object also allows us to use `ArgParse` to submit any key constants or variables - known as arguments - to the script which runs in the Azure ML environment as a Docker image. More on that later.

- Register the model `*.pkl` file/artefact to the Model Registry into Azure ML Workspace. Part of this, we will log the relevant metrics in `register.py`

!['Challenge 2 Architecture'](/Challenge23/images/challenge2architecture.png)

## <u> Steps </u>

As a team, complete the following tasks using our [Challenge 2 notebook](https://github.com/tgokal/EY-MSFTAI-Workshop3/blob/master/Challenge23/Challenge%202%20and%203.ipynb). It will also serve as our Challenge 3 notebook for continuity.

Navigate to your Challenge 2 notebook, follow the Checkpoints, instructions and # TODO sections. There will be handy SDK links to inspire you as you work through the # TODO sections.

!['Challenge 2 Notebook'](/Challenge23/images/challenge2_a.png)

For your reference, here are the high level steps of what you'll achieve in Challenge 2. These instructions are in the Challenge 2 notebook for ease of reference.

1. Within the **Challenge23** folder, create a **data** sub-folder and upload your training data CSV into it:

    !['Challenge 2 Notebook'](/Challenge23/images/challenge2_b.png)

1. Begin at **Checkpoint 1** and continue to **Checkpoint 2** **Creating the training script: train.py** section. 

    - After you run the first cell underneath the **Checkpoint** section, you should see a newly created **driver-training** folder which will contain the Experiment files, including our training data. 

    !['Challenge 2 Notebook'](/Challenge23/images/challenge2_c.png)

    - Refactor the code from the Challenge 1 notebook into a Python Script by completing the commented `##TODO` sections of the `train.py` cell in the Challenge 2 notebook.

    - Open up your Challenge 1 notebook to serve as reference of what code we ran in Challenge 1. Drag your Challenge 2 and 3 notebook to the side of the Jupyter environment to open up the notebooks side by side for ease of reference.

        !['Challenge 2 Notebook'](/Challenge23/images/challenge2_d.png)

    - Once you complete this step, you should see a new file be created in your **driver-training** file - our `train.py` file, containing our refactored functions from Challenge 1.

    - Open up the `train.py` file by double clicking it to observe what you've created from the Jupyter Notebook - all of which has been written into a Python Script. You're on your way to becoming a full-fledged machine learning engineer.
    

1. You now should have reached **Checkpoint 3** , where we need to perform Unit Tests. This ensures that our code makes sense. We pass through dummy data to our training script and expect to pass 3 tests. 

    - Drag the `test_train.py` into the **driver-training** folder:

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_f.png)  
    
    - Navigate into the **Challenge23/driver-training** folder in the Terminal

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_g.png)  

    - In the Terminal, run the command, `pip install pytest`

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_h.png)

    - Next, run the command `pytest test_train.py` in the Terminal. Learn more about [pytest in this link](https://docs.pytest.org/en/6.2.x/).

    - If you receive errors, understand which line the error was raised and resolve it from the Jupyter Notebook cell. Re-run the cell to overwrite the `train.py` file. Ask your Coach for help if you need. Learning how to debug and becoming confident as you debug is part of becoming a machine learning engineer - we see and resolve bugs everyday. Having errors pop up is common and part of the learning process.

    - Once you've resolved any error that may arise, you should see the following after running `pytest`

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_i.png)


1. At **Checkpoint 4** ensure that the `train.py` and `test_train.py` files pass linting with `flake8` in the Terminal. 

You will need to install the package from the Terminal using `pip install flake8`.

You do not need to fix every single linting error here. This is for your understanding of how to produce quality code and does not impact the output and outcome. Once you have a good understnading of what the errors mean and how you would resolve them, move on to the next step.

!['Challenge 2 Notebook'](/Challenge23/images/challenge2_j.png)

1. Complete and run the remaining cells of the Challenge 2 notebook. 

    - At **Checkpoint 5**, we create a JSON file containing the model parameters or constants that we set for model training. 
    
    These are variables that impact how quick the model trains, on what data the model trains, the complexity of the decision tree and the metric used to assess the model.

    You will see a `parameters.json` file be created in your **Challenge23/driver-training** directory:

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_k.png)
    
    - At **Checkpoint 6** In `driver_training.py`, complete the `##TODO` for using the functions imported from `train.py`. Once completed, you will see a `driver_training.py` file in your folder. Open it to review the code that you've written.

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_l.png)

    After you run the next cell, you'll see an outputs folder be created. This will store your model artefact once trained and submitted as an Experiment.

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_m.png)
    
    - At **Checkpoint 7** In the `ScriptRunConfig()` object, create a compute cluster, environment and experiment using the links provided.

    - Once you submit the Experiment run, navigate to the Azure ML workspace UI and you'll see your training run prepare:

     !['Challenge 2 Notebook'](/Challenge23/images/challenge2_n.png)

    - Training should take 10-15 minutes to complete.

    - If anything fails, you will be able to find out more information from the **Outputs + logs** section.

      !['Challenge 2 Notebook'](/Challenge23/images/challenge2_o.png)


1. View the `learning_rate` parameter in the configuration file, execute a run against Azure ML compute to train the model and verify that the metrics are logged. Change the `learning_rate` value and then execute another run and see the values changed in the Azure ML service.

1. Print out the model metrics at **Checkpoint 8**

1. Register the model in the Azure ML model repository at **Checkpoint 9** using the provided notebook code in your Azure ML workspace - using tags to record the AUC metric in the registration so that the quality of the model is registered and not just the run.

  - If you switch over to the Azure ML workspace, you'll see your registered model.

  !['Challenge 2 Notebook'](/Challenge23/images/challenge3_d.png)

## <u> Coaching Questions </u>

Once you've completed the Challenge, tag your Coach in your Team Channel and discuss the following questions with them:

1. What is the benefit of separating the training code out of the notebook?

1. What is the benefit of running your experiments using Azure Machine Learning?

1. What are the benefits of using a model repository and tracking the metrics and other parameters?

1. What is your experience in your organization/customers regarding doing things like model registration and tracking training metrics?

## <u> Success Criteria </u>  

To have completed this Challenge, you should have:  

- Have a fully functional Challenge 2 notebook (.ipynb)

    - Successfully runs your experiment on Azure ML and can see the logged AUC metrics and trained model in the run results using two different parameter configuration values.

    - Successfully registers the trained model and tags the model with the AUC metric.

- Demonstrate that the unit tests passs against the Python training code using `pytest`.

- Use `flake8` to demonstrate that `train.py` and `test_train.py` conform to the PEP 8 style guide for Python code.

- Do a local run of the notebook and show the metrics associated both with the run and the registered model in Azure ML.

- Discussed Coaching Questions with your Coach and Team.

# On to Challenge 3
Click [here](https://github.com/tgokal/EY-MSFTAI-Workshop3/blob/master/Challenge23/HOL_Challenge_3.MD) to see the HOL guide for Challenge 3. In Challenge 3, we will deploy the trained model to an Azure Container Instance. Keep your current Challenge 2 Notebook open as you'll see the Challenge 3 exercises below.
