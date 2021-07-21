# SageMaker_Tutorial

### Conceptual Steps on how to use SageMaker
* Computational task is run to perform inference on a virtual machine. 
* The Virtual Machine gets the input and the model artifacts to perform the inference task and then returns the results. 


### The Amazon Sagemaker provides the following tools:
* Ground Truth - To label the jobs, datasets, and workforces
* Notebook - To create Jupyter notebook instances, configure the lifecycle of the notebooks, and attache Git repositories
* Training - To choose an ML algorithm, define the training jobs, and tune the hyperparameter
* Inference - To compile and configure the trained models, and endpoints for deployments

### Pricing 
Sagemaker is one of the most expensive services on AWS

Particularly, the ml.p2.xlarge is almost:
* 25x more expensive than a regular t2.medium instance
* 96x more expensive than a typical t2.micro instance


Source: https://aws.amazon.com/sagemaker/pricing/

Viktor Bachraty was using SageMaker correctly (it seems). 
### Training Jobs
A training job is used to train a specific estimator.

When you request a training job to be executed you need to provide a few items:

A location on S3 where your training (and possibly validation) data is stored,
A location on S3 where the resulting model will be stored (this data is called the model artifacts),
A location of a docker container (certainly this is the case if using a built in algorithm) to be used for training
A description of the compute instance that should be used.


# Updating a Model 
We need to update the current Logistic Regression model due to Concep Drift.
1. Download the data 
2. Prepare and split the data
3. Upload the training and validation files to S3 
    * Save data to local notebook instance
    * Upload to S3 
      * Use the `upload_data` method of the `session` object.
4. Train the model 
  a) Create an estimator object which will use the XGBoost container for training. 
    * To construct an estimator, we need to provide the location of a container which contains the training code. 
    * `get_image_uri` constructs the image we need for the training container. 
    * To use this method, we need to provide it with our current region, which can be obtained from the session object, as well as the name of the algorithm we wish to use.  
    * We should also specify where to store the output and the training instance type. 
  b) Set new hyperparameters
    * Set `training_params`
    * We need the URI to the docker container that contains the XGBoost algorithm
    * We need to specify the role (ARN role) that the virtual machine that we eventually create should have. Now we specify the training image and we do this by giving a link to th container. 
    * We need to specify where the resulting model should be saved. The output of the algorithm is called the model artifacts. These are the pieces of data that were created during the training process.
    * Next, describe the properties of the virtual machine that we use for our algorithm - `training_params['ResourceConfig']`, `training_params['StoppingCondition']`. 
    * Every traning job must have a unique name. We can do that by appending a timestamp at the end of the name.  
  c) Call the `fit` function to fit our model to our training and validation data. 
  d) Create a data structure that specifies which container should be used for inference and in addition points to the model artifacts that we created earlier 
  e) Ask SageMaker to create the model
  f) Test the model 
    * We can use SageMaker's Batch Transform functionality. 
    * We build a transformer object from our `fit` model. 
    * We have to name our transform job with a unique name (use timestamps as suffix). 
    * Specify under `TransformOutput` the `S3OutputPath` to the S3 bucket where the results of our batch transformed job will be stored. 
    
    
### Deploying the Model 
1. Once we have a model, we create an endpoint configuration with a single production variant. 
  * We can simply call the `deploy` method of the trained model object making sure to specify the number of virtual machines we want to use and the type of virtual machine. 
  * When a model is deployed, SageMaker creates a virtual machine that can be accessed at an endpoint (VM hosts the trained model), i.e. at a specific URL. The return object from the `deploy` function takes care of that for you. 
  * An endpoint requires a unique name. We can append a timestamp as a suffix to accomplish this. 
  * An endpoint acts as a uniform resource that we can send data to. SageMaker can take the data that was sent to the endpoint and if we wanted to, split it up among different models. 
3. Once we have an endpoint configuration, we can ask SageMaker to create an endpoint with those properties. 
4. Test endpoint to make sure it's working 
  
  
  
"Model" as understood by SageMaker is a collection of information including any model artifacts created during training and additional information describing how the model artifacts should be used. 
  
5.  
  * T
