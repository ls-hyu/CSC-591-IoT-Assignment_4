# CSC-591-IoT-Assignment_4

## Description
* status_prediction.py: The IMU(MPU-6050) connected on the rapsberry pi detects the Gx, Gy, Gz, Ax, Ay, Az and send to the model through svm_copy.py for prediction.
* svm_copy.py: Parses the data collected, uses the model to predict and returns the predicted door status in three states, open/stable/closed.

## How to collect the data for model training?
```
$python collect_data.py.py
```

## How to train the libsvm model?
```
$pip3 install libsvm-official
$python svm.py
```
If you ran into error such as (ERROR: Could not build wheels for scipy which use PEP 517 and cannot be installed directly), try update pip.
```
$pip3 install --upgrade pip
```

## How to run it?
1. Run `python status_prediction.py` on Raspberry Pi
2. Set up IBM Cloud by instruction in IBM Cloud Testing  
3. Opens/closes the door
4. The prediction results(open/stable/closed) will show on the console


# SVM_Classification.py

This code fundamentally performs 3 functions
  * Reads the IMU Sensor data and formats the data appropriately
  * Reduces dimensionality using Principal Component Analysis
  * Classifies sensor data as door open / close using SVM (RBF)

## Pre-Requisites

Sci-kit learn library - `pip install sklearn`
Matplotlib - `pip install matplotlib`
numpy - `pip install numpy`
pandas - `pip install pandas`

Expects the IMU sensor data in the following format where the first column is door open/close indicator followed by 6 degrees of IMU data

![image](https://user-images.githubusercontent.com/99939969/163088477-248671c8-7ca0-40e2-8490-db04a0162b18.png)

### Dimensionality Reduction

The IMU sensor used in this project provides 6 features(accelaration and position along x,y,z axis). Using explained_variance_ratio, it can be noted that ~98% of the information is present in the first two features of the sensor data as shown below. We can therefore, reduce the no. of features from 6 to 2 using principal component analysis.

![image](https://user-images.githubusercontent.com/99939969/163089470-fd9e5127-a106-44f1-941a-7117c7fb9584.png)

### Classification
Classification is performed using Support Vector Machine(SVM) RBF method. The optimum C and gamma values are resolved using GridSearch. Optimum C and gamma values were found to be C=1, gamma = 0.12 for this example dataset. The decision boundary between door open and close (+1 and -1 respectively) can be identified as shown in the plot below. Approximately 50% of the training data is used for testing and predicts the door open/close status with 89% accuracy.

![image](https://user-images.githubusercontent.com/99939969/163090475-f26d344a-f884-4967-b118-20ccfc99500b.png)









