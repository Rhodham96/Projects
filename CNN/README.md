# Image Recognizer using CNN

This project demonstrates the implementation of a Convolutional Neural Network (CNN) for image recognition, specifically for classifying images of bikes and cars.

## Project Structure

The project is organized as follows:

- **datasets:** This folder contains the training, validation, and test datasets. The datasets are organized into subfolders for each class (Bike and Car).
    - **Train:** Contains the training dataset.
    - **Val:** Contains the validation dataset.
    - **Test:** Contains the test dataset.
- **results_Bike:** Contains the feature maps for the Bike images.
- **results_Car:** Contains the feature maps for the Car images.
- **logs:** Contains the TensorBoard logs.

## Data Preparation

1. **Download and Extract Datasets:** The code downloads zip files containing images of bikes and cars and extracts them into the `datasets/Train` directory.
2. **Split Datasets:** The code splits the datasets into training, validation, and test sets. It randomly selects a portion of the images from the `Train` directory and moves them to the `Val` and `Test` directories.
3. **Data Loading:** The code uses the `ImageFolder` class from `torchvision` to load the images and labels from the datasets. It also applies transformations to the images, such as resizing and converting them to tensors.

## Model Architecture

The code defines a CNN model using the `nn.Module` class from PyTorch. The model consists of several convolutional layers, max pooling layers, and fully connected layers.

## Training

The code trains the model using the training dataset and the Adam optimizer. It also uses TensorBoard to visualize the training progress.

## Evaluation

The code evaluates the model on the test dataset and displays the accuracy. It also displays the feature maps of the convolutional layers for a few randomly selected images.

## Usage

To run the project, simply open the notebook in Google Colab and execute the cells in order.

## Acknowledgements

This project is inspired by various tutorials and resources available online.
