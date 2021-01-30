# Wide and Deep Neural model for structure data

In this notebook we will cover how to create Wide and Deep model for strcutured data with tf.keras layers with below tensorflow features. I will also share references like youtube videos & notebooks which has inspired this work.


- Tensorflow Dataset API
- Distributed strategy
- Tensorboard for experiment tracking
- Tensorflow profiling
- visualizing keras Model 
- Feature Engineering
  - One-Hot encode of categorical attributes
  - Feature crossing



# Dataset API

- **Interleave**: to process many input file concurrently
- **map** : to apply pre-processing function parallelly to dataset
- **Prefecth** : once a batch is dispatched for model training CPU is Idle, Prefecth will start working on next batch as soon as data has been dispatched for model traning 

**Note: Number of parallel call is also hyperparameter to select correct value automatically use tf.data.experiment.AUTOTUNE**

![Screenshot](../images/dataset1.PNG)
