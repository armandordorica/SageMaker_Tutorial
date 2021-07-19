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


### Training Jobs
A training job is used to train a specific estimator.

When you request a training job to be executed you need to provide a few items:

A location on S3 where your training (and possibly validation) data is stored,
A location on S3 where the resulting model will be stored (this data is called the model artifacts),
A location of a docker container (certainly this is the case if using a built in algorithm) to be used for training
A description of the compute instance that should be used.
