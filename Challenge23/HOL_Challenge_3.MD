# Welcome to Challenge 3


## Aim

You just transformed the experimental notebook into a Python script that can be managed and run independently of the notebook environment. You used the script to train the model, then you used code in the notebook to register the model that the script produced. 

To keep the training, registration and future steps like evaluation as easily reproducible as possible, we can encapsulate the model training and registration steps in an Azure ML pipeline which utilizes provisioned on-demand scalable Azure compute targets. The Azure compute target optimizes the time spent running training with a full set of data and can scale down to no cost when the job is done.

In order to improve the insurance application, we can use a real-time prediction of the likelihood that a driver will file a claim. To accomplish this objective, we'll be deploying the registered model as a real-time inferencing REST service using the provisioned model scoring script.

!['Challenge 3 Architecture'](/Challenge23/images/challenge3architecture.PNG)

In this Challenge, we will:

- Retrieve the most recent version of the registered insurance claim prediction model.

- Create a socring script which includes an `init` function that loads the registered model and a `run` function that uses it to predict claim classifications for new driver data.

- Define the container environment that includes the Python packages required by your scoring script.

- Deploy the model as an Azure Container Instance service.

- Testing the deployed service by submitting a REST request to its endpoint and review the predictions it returns.

## Getting Started

Follow along in the Challenge 2 and 3 Jupyter Notebook which contains the instructions for creating and testing the REST API endpoint.

## Success Criteria

- Define the `run` function for the scoring script which will call the model predictions and returns the probabilities and predicted classes.

- Add the model dependencies into the container environment.

- Define the InferenceConfig() which is used to deploy the model to Azure Container Instances.

- Successfully deploy the trained model as a REST service in Azure Container Instance and test its endpoint.

## Coaching Questions

- What are the benefits of splitting the ML process into steps?

- What are the benefits of using the InferenceConfig object for deployment?


