# GAN_trafficsign_recognition

1) Data
2) Dataset Creation and Preprocessing
3) Classifier Models

1. Data:

The data came from the German Traffic Sign Dataset (pickled files found here: https://d17h27t6h515a5.cloudfront.net/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip)

This dataset contains 50,000+ images in 43 classes and was used for the Traffic Sign Recognition (TSR) classifier as well as the combined TSR+CIFAR10 classifier. I used CIFAR10 images as a "not a sign" class for some of the models: https://www.cs.toronto.edu/~kriz/cifar.html

Both datasets were in 32x32 RGB format.  The data for both the full TSR+CIFAR dataset as well as the TSR-only dataset were divided into 67% training, 8% validation, and 25% testing datasets with classes remaining at the same class percentage in each set.

Class Breakdown in TSR Datasets:

Training set is: (36699, 32,32,3) + labels column

![Alt text](images/train.png?raw=true "Training Set Class Breakdown")


Test set is: (13313, 32,32,3) + labels column

![Alt text](images/test.png?raw=true "Test Set Class Breakdown")


Validation set is: (4645, 32,32,3) + labels column

![Alt text](images/valid.png?raw=true "Validation Set Class Breakdown")

2. Dataset Creation and Preprocessing

"dataset_creation/TSRGAN_dataprep.ipynb" contains code which pulls the German Traffic sign images as well as random CIFAR10 images, putting the CIFAR10 images under one class label.  We first tried to create a model that would overfit and learn on a small, 3-class dataset containing two signs and the "not a sign" class.  This code generated numpy arrays for the 3-class dataset as well as the "all-class" datasets.

Preprocessing steps taken:

*shuffle

*grayscale

These steps are found in the classifier codes.

3. Classifier Models

3-Class (TSR + CIFAR) Models:

I used a model, LeNet-5, which was successful in classifying the German traffic sign dataset (https://github.com/mohamedameen93/German-Traffic-Sign-Classification-Using-TensorFlow).  While I was able to overfit the model, I was unable to increase the validation/test accuracy when the CIFAR images were included.  This training model was expanded to the full traffic sign + CIFAR dataset but was still not found to classify the test/validation sets accurately, even after regularization steps were taken.

I also tried a general fully connected neural network on the 3-class dataset. "fully_connected_classifier/FC_NN_classifier.py" refers to the fully connected (FC) neural network (NN) which was developed to classify between 3 classes (2 traffic signs + a "not-a-sign" class consisting of various CIFAR images). "fully_connected_classifier/tf_utils.py" contains the mini-batch generator and convert-to-one-hot functions used in FC_NN_classifier.py.

TSR Models:

Using LeNet-5 and various regularization methods, I was able to classify all 43 classes in the German Traffic sign dataset with a validation accuracy of 95.2% and test accuracy of 91.2%.  These numbers could be improved, but were high enough to serve its purpose as the target classifier of the Attack-GAN network.
