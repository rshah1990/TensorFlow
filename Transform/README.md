# Tensorflow Transform (tf.transform)

- when doing pre-processing in tensorflow , it has to be completely depends on the input data to the model
- one of the example of it is one-hot encoding of categorical column which is completely depends on the current input. tensorflow model is stateless. 
- what if you need average of the last 7 day as an input feature that requires query the production database to fetch last 7 days of data & average it out
- this cant be done in tensorflow since in tensorflow pre-processing is part of tensorflow graph 
- Another way to do pre-processing is using Apache beam in stateful way where you can write arbitrary python code (moving average of last 7 days), its auto-scalable which is useful when you have very large training data 
- but what if you want just scale the data using min max scalar & get vocab list from bunch of text. if data is very large than distributed pre-processing will help you to fasten the process but we have to use this during inference as well 
- thats when tensorflow transforms comes in , its in-between the tensorflow pre-processing & apache beam.
- tf.transform is hybride of beam & tensorflow. it runs training (large data) pre-processing in Apache beam & inference (small data) pre-processing in tensorflow.
- since inference code will be part of tensorflow graph , pre-processing function must include tensorflow variables & transformation 
- tf.transforms provides two Ptransforms method. which is very similar to sklearn fit_transform & transform function  
  - AnalyzeAndTransformDataset : Executed in Beam to create training dataset
  - TransformDataset: executed in beam to create evaluation dataset 

# Code flow 

- Setup training schema: information to Apache beam to understand training data schema
- Analyze & transform: returns pre-processed training data & transform function 
- Dump transformed Data: efficient way to write it as TF records
- Pre-processing function:
   - this will be part of serving input function during inference ie. will be added in tensorflow graph & executed during tensorflow serving 
   - since its part of serving input function its restricted with the function which can be called from tensorflow. cant write arbitrary python code
- Pre-processing in evaluation dataset: reuse the transform function returned during training & dump it also in Tfrecords
- Transformation metadata: dump the transformation metadata, which will be part of serving input function 
- Serving input function: load transformed function & create serving input function , this will be part of estimator
