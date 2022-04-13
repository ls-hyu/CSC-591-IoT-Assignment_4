# CSC-591-IoT-Assignment_4
# status_prediction_.py
# svm_copy.py

## Description
* status_prediction.py: The IMU(MPU-6050) connected on the rapsberry pi detects the Gx, Gy, Gz, Ax, Ay, Az and send to the model through svm_copy.py for prediction.
* svm_copy.py: Parses the data collected, uses the model to predict and returns the predicted door status in three states, open/stable/closed.

## How to run it?
1. python status_prediction.py
2. Opens/closes the door
3. The prediction results(open/stable/closed) will show on the console
