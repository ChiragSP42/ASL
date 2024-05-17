# Real-time Hand Sign Detection:

The project aims to detect ASL (American Sign Language) alphabets in real-time. To do this we will be using Google's Mediapipe library to identify the hand and draw landmarks. Using the coordinates of these 21 landmarks, we train a Random Forest model. The model performs excellently with a few misclassifications between the 'R' and 'T' hand signs due to their similar nature. A more detailed explanation for this is given below. As with any project, it is divided into 3 sections, Data collection, model training and real time execution.

## Data Collection

We will be using OpenCV for collecting images from webcam. Each image is passed to the mediapipe hand model which draws the 21 landmarks. The coordinates of the landmarks are stored as a CSV file. For diversification, both hands are recorded at a time totalling 2000 rows, 1000 rows each. For modularity, the current working directory+folder to store csv files format is used. This can be easily changed as the need is required. Other parameters that can be altered is total number of data points to be collected, number of data points to be taken for each hand (note is has to be symmetrical).

## Training Model

I decided to try Random Forest and SVC as they would treat each XY coordinate as a separate dimension. I started with Random Forest as it can handle large number of features and is non-parametric, and the test evaluation metrics came out spendidly. The model gave an overall accuracy of 98% with default hyperparameters and an average precision and recall of 97%. I stored the model as a pickle file which is of ~170MB.

## Real-time execution:

Again OpenCV is used to gather images in real-time, mediapipe is used to identify landmark coordinates and is fed to the trained model. A dictionary of prediction-letter is used to convert the predictions of the model into the corresponding letter.

## Improvements:

* As mentioned above there is a misclassification of letter 'R' and 'T' hand signs due to their similar nature. One way to reduce this would be to increase the number of data points recorded for these two classes.
* Another possible improvement is that OpenCV is fragile and any unforseen errors leads to the window freezing with no option other than to restart the kernel. Further research is required if it is to be a standalone application.
