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

- export using tf.saved_model.save function, it will export it as pre-defined structure for each version you mention.
  - model as protobuf (saved_model.pb)
  - asset contains additional files like vocabulary 
  - variables and checkpoints
<img src="serving/export_folder.PNG" width="400">

  
## Serve with Docker
- docker images are available for CPU & GPU.
- pull docker image -> run docker image with "docker run" command with certain parameters
    - docker run -p 8501:8501 
            --mount type=bind,
             source=/path/to/my_model/
             target=/models/my_model 
            -e MODEL_NAME=my_model 
            -t tensorflow/serving 
- to run it for GPU , just change container name
- it will create two end point one with gRPC and one for REST
