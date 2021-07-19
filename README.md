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
