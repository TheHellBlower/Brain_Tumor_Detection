# Brain Tumor Detection using VGG-16

## Project Motivation
The aim of this project is to use Computer Vision techniques of Deep Learning to correctly identify and map Brain Tumors for assistance in Robotic Surgery. This project builds a CNN model to classify whether a subject has a tumor or not based on an MRI scan.

## Dataset
The dataset consists of MRI scans of two classes:
* **NO**: No tumor, encoded as `0`.
* **YES**: Tumor, encoded as `1`.

The dataset is split into training, validation, and test sets with the following structure:
* **Training set**: 193 images
* **Validation set**: 50 images
* **Test set**: 10 images
* **Total images**: 253

## Preprocessing
The following preprocessing steps were used:
* Images were resized to 224x224 pixels.
* Data augmentation was applied to the training data using `ImageDataGenerator` with the following transformations:
    * `rotation_range=15`
    * `width_shift_range=0.1`
    * `height_shift_range=0.1`
    * `shear_range=0.1`
    * `brightness_range=[0.5, 1.5]`
    * `horizontal_flip=True`
    * `vertical_flip=True`

## Model Architecture
A VGG-16 model pre-trained on ImageNet was used as the base, with the following modifications:
* The original classification layers of VGG-16 were frozen.
* A custom classifier was added on top of the VGG-16 base:
    1.  **Flatten** layer
    2.  **Dense** layer with 128 neurons and a **ReLU** activation function.
    3.  **Dense** layer with 2 neurons and a **softmax** activation function.
* **Optimizer**: Adam with a learning rate of 1e-5.
* **Loss Function**: Categorical cross-entropy.

## Training Details
* **Epochs**: 20
* **Batch Size**: 32
* The model was trained with an `EarlyStopping` callback to monitor the validation accuracy and stop training if there was no improvement after a certain number of epochs.
* **Final Training Accuracy**: 98.96%
* **Final Validation Accuracy**: 100%

## Evaluation Metrics
The model's performance was evaluated using the following metrics:
* **Confusion Matrix**: A confusion matrix was plotted to visualize the model's predictions on the test set.
* **Accuracy Score**: The overall accuracy of the model on the test set was calculated.
* **Precision, Recall, and F1-Score**: These metrics were not explicitly calculated in the notebook, but the confusion matrix provides the data to derive them.

## Results & Conclusions
The model achieved an accuracy of **100%** on the test set. The confusion matrix shows that all 10 test images were classified correctly. This indicates that the VGG-16 based model with transfer learning is highly effective for this binary classification task of brain tumor detection from MRI scans.
