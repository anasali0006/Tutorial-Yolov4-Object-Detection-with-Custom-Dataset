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
3. Execute the first cell. This will connect your google drive with the Colab Notebook. Select the account in which you have uploaded the dataset. One thing that is worth noting here is that the Google account on which Colab is running does not need to be same as the Google account in which the dataset is present (We will use this feature soon. Just hold on!)\
![image](https://user-images.githubusercontent.com/61320147/115934317-31b0d480-a4aa-11eb-9f47-dfb219dfaccc.png)
4. Executing this block will check for the nvcc version. \
![image](https://user-images.githubusercontent.com/61320147/115937208-c0c0eb00-a4b0-11eb-9db4-c286b66c8d0f.png)
5. In the next step, the 'darknet-for-colab' is cloned. I have taken this repo from the author mentioned above and made the necessary changes so it runs smoothly with latest 'nvcc' drivers. All the settings have been pre-configured so darknet runs on Colab without any issues.(Darknet is just the name of the *platform* which is used for Yolo model training). \
        *Note*: Various 'assert' statements have been added to ensure that we are in correct directory. \
        ![image](https://user-images.githubusercontent.com/61320147/115938376-db489380-a4b3-11eb-984c-38408e1b3881.png)
6. We are going to implement transfer learning here. Transfer learning means to use pre-trained model which is trained on some common classes and train it further on our class(es). This way the chances of reaching the high accuracy are more and quicker as compared to training a whole model from scratch. Therefore, we are going to download pre-trained *weights*.\ 
![image](https://user-images.githubusercontent.com/61320147/115938342-ba803e00-a4b3-11eb-9440-a306730603a1.png)
7. Next we are going to download the dataset which has been uploaded on the Google Drive. Kindly note that the current working directory is 'data'. We are going to put all the images and corresponding label-text files in the folder named *ts*. (Path: /darknet-for-colab/data/ts).
The code which I have written for this part is a good strating point but it will change a little depending upon how have you zipped the images and where are you unzipping them. Just keep in mind that end goal is to have all the images and labels in the folder named *ts* inside *data* folder. \
![image](https://user-images.githubusercontent.com/61320147/115940626-b22c0100-a4bb-11eb-919d-5eb4fcab7568.png)
8. 




