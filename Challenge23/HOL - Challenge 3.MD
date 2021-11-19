# Welcome to Challenge 3


## <u> Aim </u>

You just transformed the experimental notebook into a Python script that can be managed and run independently of the notebook environment. You used the script to train the model, then you used code in the notebook to register the model that the script produced. 

To keep the training, registration and future steps like evaluation as easily reproducible as possible, we can encapsulate the model training and registration steps in an Azure ML pipeline which utilizes provisioned on-demand scalable Azure compute targets. The Azure compute target optimizes the time spent running training with a full set of data and can scale down to no cost when the job is done.

In order to improve the insurance application, we can use a real-time prediction of the likelihood that a driver will file a claim. To accomplish this objective, we'll be deploying the registered model as a real-time inferencing REST service using the provisioned model scoring script.


In this Challenge, we will:

# TODO 

