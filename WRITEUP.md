# Project Write-Up

You can use this document as a template for providing your project write-up. However, if you
have a different format you prefer, feel free to use it as long as you answer all required
questions.

## Explaining Custom Layers

The process behind converting custom layers involves.

- Obtaining model, preprocessing input and handling output.
- Using a model optimizer to generate intermediate representation of custom layers.
- Run the model in OpenVino framework using cutom layers.

Some of the potential reasons for handling custom layers are, sometimes IR deosn't support the original model. So we need to modify the using custom layers.

I used Tensorflow object detection model zoo to select an appropiate model. This can be found in the following link:
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md

I chose 'ssd_mobilenet_v2_coco' for this project. However I tried 'faster_rcnn_inception_v2_coco' which was slower in execution.

To download 'ssd_mobilenet_v2_coco' we use the following command:

wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz

Then we use 'tar -xvf' to exract it.

tar -xvf ssd_mobilenet_v2_coco_2018_03_29.tar.gz

We convert the model to generate .xml and .bin files using the following command:

python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --reverse_input_channels --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json

The IR models can be found in 'model' folder. Execution took about 70 seconds.

## Comparing Model Performance

My method(s) to compare models before and after conversion to Intermediate Representations
were.

The difference between model accuracy pre- and post-conversion was the 'ssd_mobilenet_v2_coco' IR model is faster than 'faster_rcnn_inception_v2_coco', however it was less accurate in counting if the subject was static and wearing dark colored clothes.

The size of the model pre- and post-conversion was:
'ssd_mobilenet_v2_coco' size-before: 66 MB (.pb) file) size-after: 65 MB

The inference time of the model pre- and post-conversion was about 70 ms.

## Assess Model Use Cases

Some of the potential use cases of the people counter app are:

Due to the unfortunate outbrake of COVID-19 it is necessary to restric socia gathering to public places like retail shop, restaurants etc. 

Each of these use cases would be useful because,

With a people's counter app we can keep track of people entering and leaving so that we can limit social gathering. 

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. The potential effects of each of these are as follows:

Lightning and focal length can change model accuracy. a well balanced lighting and clear image can improve detection accuracy.

Image size should be comaptible as well. If the person is not in the frame properly, it will difficult to draw a bounding box, which will affect model accuracy.


## Model Research

[This heading is only required if a suitable model was not found after trying out at least three
different models. However, you may also use this heading to detail how you converted 
a successful model.]

In investigating potential people counter models, I tried each of the following three models:

- Model 1: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...
  
- Model 2: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...

- Model 3: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...
