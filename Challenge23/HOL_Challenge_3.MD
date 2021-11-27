# Welcome to Challenge 3


## Aim

You just transformed the experimental notebook into a Python script that can be managed and run independently of the notebook environment. You used the script to train the model, then you used code in the notebook to register the model that the script produced. 

To keep the training, registration and future steps like evaluation as easily reproducible as possible, we can encapsulate the model training and registration steps in an Azure ML pipeline which utilizes provisioned on-demand scalable Azure compute targets. The Azure compute target optimizes the time spent running training with a full set of data and can scale down to no cost when the job is done.

In order to improve the insurance application, we can use a real-time prediction of the likelihood that a driver will file a claim. To accomplish this objective, we'll be deploying the registered model as a real-time inferencing REST service using the provisioned model scoring script.

!['Challenge 3 Architecture'](/Challenge23/images/challenge3architecture.PNG)

In this Challenge, we will:

- Retrieve the most recent version of the registered insurance claim prediction model.

- Create a scoring script which includes an `init` function that loads the registered model and a `run` function that uses it to predict claim classifications for new driver data.

- Define the container environment that includes the Python packages required by your scoring script.

- Deploy the model as an Azure Container Instance service.

- Testing the deployed service by submitting a REST request to its endpoint and review the predictions it returns.

## Getting Started

Follow along in the Challenge 2 and 3 Jupyter Notebook which contains the instructions for creating and testing the REST API endpoint.

1. At **Checkpoint 1**, we retrieve the most recent version of our registered insurance claim prediction model. 

    - From the following cell, you should see a `driver-service` folder which will contain all of your web service files that will be deployed to your deployment compute type.

    !['Challenge 3 Architecture'](/Challenge23/images/challenge3_a.png)

2. Complete the # TODO in the cell for **Checkpoint 2** - write a for-loop which appends the labels based on logic of sorting the probabilities.

    - Once you run the cell, you will see your `score_driver.py` file in the `driver-service` folder. Open the file to review the code you've added to. 

    !['Challenge 3 Architecture'](/Challenge23/images/challenge3_b.png)

3. In **Checkpoint 3**, we define the Container Environment through a YAML file. Complete the # TODO in the below cell.

    - Once you complete it, you'll see the environment YAML file:

    !['Challenge 3 Architecture'](/Challenge23/images/challenge3_c.png)

4. Define the `InferenceConfig()` at **Checkpoint 4** and configure the scoring environment.

    - This will create an endpoint which will be in transitioning state for around 10-15 minutes.

    !['Challenge 2 Notebook'](/Challenge23/images/challenge3_e.png)

5. By **Checkpoint 5** you should have deployed a a webservice to Azure ML and now that we will submit data to the endpoint and retrieve the predictions. In the next cell, we'll repeat this but for multiple drivers.

6. **Checkpoint 6** allows us to submit the data to the endpoint using `requests.post()`.

## Coaching Questions

- What are the benefits of splitting the ML process into steps?

- What are the benefits of using the InferenceConfig object for deployment?

## Success Criteria

- Define the `run` function for the scoring script which will call the model predictions and returns the probabilities and predicted classes.

- Add the model dependencies into the container environment.

- Define the InferenceConfig() which is used to deploy the model to Azure Container Instances.

- Successfully deploy the trained model as a REST service in Azure Container Instance and test its endpoint.

- Discussed the Coaching Questions with your Coach and Team.

# On to Challenge 4
Click [here](https://github.com/tgokal/EY-MSFTAI-Workshop3/blob/master/Challenge4/HOL_Challenge_4.MD) to see the HOL guide for Challenge 4. In Challenge 4, we will create our model's CICD pipeline in Azure DevOps.


