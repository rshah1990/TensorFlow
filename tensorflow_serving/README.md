# Tensorflow Serving 

- Deployment of tensorflow model can be done in two way. Flask or Tensorflow serving 
- traditional way of deploying model is using flask but its really inefficent way of doing it.
  - no consistent API & payload
  - No model versioning 
  - No mini batch support 
  - Inefficent for large model
- Tensorflow server is production ready model serving solution 
  - works well for large model upto 2 GB (probuf has limit)
  - part of TFX 
  - highly scalable for model serving solution

## Model export

- export using tf.saved_model.save function, it will export it as pre-defined structure for each version you mention 
- 
  