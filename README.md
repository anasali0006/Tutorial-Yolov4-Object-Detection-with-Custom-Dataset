# Yolov4-Object-Detection-with-Custom-Dataset(Google Colab)

The following tutorial is being written for the people who have smaller background knowledge in Deep Learning techniques but want to train their Yolo Models easy way. 

This tutorial is based on the article by Quang Nguyen which can be accessed from [here](https://towardsdatascience.com/yolov4-in-google-colab-train-your-custom-dataset-traffic-signs-with-ease-3243ca91c81d). I have just tried to made things a little easier for newbies, but you are highly encourarged to read the above mentioned article for better understanding and give the writer thumbsup. 

Lets dive in.

We will be using Google Colab for the training of our model YOLOv4. Google Colab provides us with free access to 12GB NVIDIA T4 GPU for a limited amount of time. We can use this free resource to our benefit and speed up our model training. Please keep in mind that once we start training of the model as big as YOLOv4, we will only be able to use if for some time and automatically be temporarily blocked by google. But don't worry about it. We will see how this issue can be tackled to some extent. 

## Prerequisites
The only prerequisite that we have here is the dataset. You should have your dataset labelled in the YOLO format. Just a little info about Data Labelling in Yolo format:
* The label-text file's name is same as image-file's name
* Label-text file will be formatted like <object_class> <x_center> <y_center> <width.> <height.>

If you have your dataset labelled in some other format, it can easily be converted to Yolo format. Just Google it. 

