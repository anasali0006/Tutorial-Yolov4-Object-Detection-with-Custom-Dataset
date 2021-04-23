# Yolov4-Object-Detection-with-Custom-Dataset(Google Colab)

The following tutorial is being written for the people who have smaller background knowledge in Deep Learning techniques but want to train their Yolo Models easy way. 

This tutorial is based on the article by Quang Nguyen which can be accessed from [here](https://towardsdatascience.com/yolov4-in-google-colab-train-your-custom-dataset-traffic-signs-with-ease-3243ca91c81d). I have just tried to made things a little easier for newbies, but you are highly encourarged to read the above mentioned article for better understanding and give the writer thumbsup. 

Lets dive in.

We will be using Google Colab for the training of our model YOLOv4. Google Colab provides us with free access to 12GB NVIDIA T4 GPU for a limited amount of time. We can use this free resource to our benefit and speed up our model training. Please keep in mind that once we start training of the model as big as YOLOv4, we will only be able to use if for some time and automatically be temporarily blocked by google. But don't worry about it. We will see how this issue can be tackled to some extent. 

## Prerequisites
The only prerequisite that we have here is the dataset. You should have your dataset labelled in the YOLO format. Just a little info about Data Labelling in Yolo format:
* The label-text file's name is same as image-file's name
* Label-text file will be formatted like <object_class> <x_center> <y_center> <width.> <height.>

If you have your dataset labelled in some other format, it can easily be converted to Yolo format. Just Google how to do it.

Plus zip your dataset and upload it to Google Drive so it can be easily accessed from the Colab.

Just one last thing before we go for training. Create a folder in Google Drive where we will store the backup of the training results in case the training is interrupted and we don't want to start from scratch. 

## Training
1. Open the Google Colab Notebook [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]()
2. Make sure you are connected to GPU Runtime. This is achieved by going to "Edit -> Notebook Settings" and setting the hardware accelerator to GPU. 
3. Execute the first cell. This will connect your google 
![image](https://user-images.githubusercontent.com/61320147/115934317-31b0d480-a4aa-11eb-9f47-dfb219dfaccc.png)


