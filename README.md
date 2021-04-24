# Yolov4-Object-Detection-with-Custom-Dataset(Google Colab)

The following tutorial is being written for the people who want to train their Yolo Models easy way. 

This tutorial is based on the article by Quang Nguyen which can be accessed from [here](https://towardsdatascience.com/yolov4-in-google-colab-train-your-custom-dataset-traffic-signs-with-ease-3243ca91c81d). I have just tried to made things a little easier for newbies, but you are highly encourarged to read the above mentioned article for better understanding and give the writer thumbsup. 

Lets dive in.

We will be using Google Colab for the training of our model YOLOv4. Google Colab provides us with free access to 12GB NVIDIA T4 GPU for a limited amount of time. We can use this free resource to our benefit and speed up our model training. Please keep in mind that once we start training of the model as big as YOLOv4, we will only be able to use if for some time and automatically be temporarily blocked by google. But don't worry about it. We will see how this issue can be tackled. 

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
![image](https://user-images.githubusercontent.com/61320147/115934317-31b0d480-a4aa-11eb-9f47-dfb219dfaccc.png)\
For those of you who are new to Colab, the directory structure of the Colab can be accessed from clicking that folder icon on the left side of the page. You will observe that after the Google Drive is attached, a directory named *drive* has appeared. You can access your Google Drive from *drive/MyDrive/*. Another thing to note is that default directory is */content/*. For example, the complete path of Google Drive is */content/drive/MyDrive/...* \
![image](https://user-images.githubusercontent.com/61320147/115941407-ad1c8100-a4be-11eb-9937-6949ee5f59b2.png)

4. Executing this block will check for the nvcc version. \
![image](https://user-images.githubusercontent.com/61320147/115937208-c0c0eb00-a4b0-11eb-9db4-c286b66c8d0f.png)

5. In the next step, the 'darknet-for-colab' is cloned. I have taken this repo from the author mentioned above and made the necessary changes so it runs smoothly with latest 'nvcc' drivers. All the settings have been pre-configured so darknet runs on Colab without any issues.(Darknet is just the name of the *platform* which is used for Yolo model training). \
        *Note*: Various 'assert' statements have been added to ensure that we are in correct directory. \
        ![image](https://user-images.githubusercontent.com/61320147/115938376-db489380-a4b3-11eb-984c-38408e1b3881.png)

6. We are going to implement transfer learning here. Transfer learning means to use pre-trained model which is trained on some common classes and train it further on our class(es). This way the chances of reaching the high accuracy are more and quicker as compared to training a whole model from scratch. Therefore, we are going to download pre-trained *weights*.\ 
![image](https://user-images.githubusercontent.com/61320147/115938342-ba803e00-a4b3-11eb-9440-a306730603a1.png)

7. Next we are going to download the dataset which has been uploaded on the Google Drive. Kindly note that the working directory here is '/darknet-for-colab/data'. We are going to put all the images and corresponding label-text files in the folder named *ts*. (Path: /darknet-for-colab/data/ts).
The code which I have written for this part is a good strating point but it will change a little depending upon how have you zipped the images and where are you unzipping them. Just keep in mind that end goal is to have all the images and labels in the folder named *ts* inside *data* folder. \
![image](https://user-images.githubusercontent.com/61320147/115940626-b22c0100-a4bb-11eb-919d-5eb4fcab7568.png)


8. So far so good? Perfect! Now is the time to look a little bit about changes that need to be done according to your own datasets. The following changes need to be made insde *data* directory:
    * Edit *yolov4.data*. Double click the file and it will open. Specify the number of classes that you wish to train the model for. And provide the path to backup folder. Kindly ensure that backup folder is in Google Drive so that backup data is permanently stored. In my code, you will see the example. Ctrl+S for save and we are good to go.
    * Create a file named *classes.names* and in each line enter the name of the class for which you are training the model. I was doing for pistols, so I added *pistol* to this file. \
       ![image](https://user-images.githubusercontent.com/61320147/115941857-bdcdf680-a4c0-11eb-8b18-28fc6cc7b1dc.png) \
    * Create empty files named *test.txt* and *train.txt*

9. Then we have to populate the *test.txt* and *train.txt* with test and train images names. I have provided code that will do that. In my code, 1000 images are being put into *test.txt*. You are free to change the number depending upon your dataset. \
![image](https://user-images.githubusercontent.com/61320147/115941985-3a60d500-a4c1-11eb-9298-eb96f6889ca7.png)\

10. Getting tired? We are just around the corner! Now its time to create a custom configuration or *cfg* file for training of your model. *cfg* file contains all the necessary information which model needs for its training like number of iterations, batch-size, learning-rate etc. Before running the cell below, open the file named *yolov4_setup.py*. Here spend some time to make changes:
       * Change number of classes as we did previosly
       * I would recommend changing the max_batches from 8000 to 3000. Max_batches refer to total number of training iterations. 
       * Change width and height accordingly. For most applications, 416 x 416 size is sufficient. 
       * If you have changed max_batches, also change the *steps* accordingly. These are the number of iterations after which learning rate decays. \
       * ![image](https://user-images.githubusercontent.com/61320147/115942294-f373df00-a4c2-11eb-9402-4628e116e7a7.png) \
After applying the above changes, run the cell below. 
![image](https://user-images.githubusercontent.com/61320147/115942138-25d10c80-a4c2-11eb-8f8e-c28d2dc34461.png)

This will generate a *cfg* file at */content/darknet-for-colab/cfg/yolov4_custom_train.cfg*. You can open the file and have a look. If you wish to edit something, it can also be done here. The meanings of parameters in *cfg* file can be found [here](https://github.com/AlexeyAB/darknet/wiki/CFG-Parameters-in-the-%5Bnet%5D-section)

11. Now running the next cell will start the model training. \
![image](https://user-images.githubusercontent.com/61320147/115942420-a80e0080-a4c3-11eb-9bc4-4681991b1aa8.png)
It can be noted here that we have provided three things to the model
       * data/yolov4.data 
       * cfg/yolov4_custom_train.cfg 
       * yolov4.conv.137 (pre-trained weights)
 
Congrats! You have successfully started the model training!

12. When the training is complete, file named *chart.png* will appear in the *darknet-for-colab* which will contain the loss/accuracy graph for training. But that usually takes a lot of time. You can keep an eye on the loss value from time to time and if it is around 1, the training is good enough. In the following figure, highlighted are the loss values. \
![image](https://user-images.githubusercontent.com/61320147/115942752-30d96c00-a4c5-11eb-8f87-1c5c0dd1c54d.png)


## Tips and Tricks
As the model is now training, it is utilizing GPU at a very fast rate. After all, YOLOv4 is quite a big model. Google will sense this high usage, and might block your access after about 5-6 hours of training. Another issue which might occur is the fact that sometimes Colab is unpredictable and can crash, causing loss of training. But worry not. We have already ensured that our backup is stored in Google Drive. This essentially means that if any of the above things happen, we can continue the training from where it broke.

For this purpose, I have created another block of code. Have a look: \
![image](https://user-images.githubusercontent.com/61320147/115942799-5ebeb080-a4c5-11eb-9f54-b22e48f9a93a.png)
Lets say your session broke due to some reason, you can reconnect and follow all the steps given above (and it will take only 2 mins once you get hang of it) except step 11. Now we have to specify the last_saved weights from our backup. When you look into the backup folder you have created on Google Drive, you will see weights files there. We need to provide path of that file and just run this cell. 

## Google Limits the Resources and its workaround
You will see that after 5-6 hours, Colab might get disconnected. And when you try to connect again, it will say you have reached GPU limitations and Google has temporarily blocked your GPUs. Either we run the model training without GPU (which would take days, if not weeks) or we can look for some workaround. Workaround here is to change the Google account from which Colab was running. Suppose you are a group of 4-5 members working on the training, when one memeber's limit is reached, login with the second member's account and you can resume the training with GPUs. Account can be changed by clicking the account icon on the top right side of page. This will change the google account associated with Colab Notebook and now this fresh account, whichh has not been restricted by Google, can be used to run colab.

One interesting thing here is even tho you are now running the Colab with new Google account, the drive you have to attach in step 1 need not to be of the same new account. This means that you can attach the old account's drive and will have access to your backup weights. Bingo! Now you have access to GPUs as well as your backup so you can resume the training. When this account gets temporarily restricted, you can switch to third Google account and again resume the training with GPUs. 

I hope it helps. 

If you have any questions, feel free to ask! 
     







