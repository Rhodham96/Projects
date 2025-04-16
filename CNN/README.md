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

## Feature Map Visualizations

The project includes visualizations of the feature maps extracted from the convolutional layers of the CNN model. Feature maps represent the activations of the convolutional filters at different layers of the network. They provide insights into how the model learns to identify features in the input images.

### Visualization Process

The following steps are involved in visualizing the feature maps:

1. **Hooking into the Model:** A hook is attached to the desired convolutional layer to capture its output (activations) during the forward pass.
2. **Forward Pass:** An input image is passed through the model, and the activations of the hooked layer are stored.
3. **Processing Activations:** The activations are detached from the computation graph and converted to NumPy arrays for visualization.
4. **Plotting Feature Maps:** The feature maps are plotted as individual images, arranged in a grid. Each image in the grid represents the activation of a different filter in the convolutional layer.

### Interpretation

By examining the feature maps, we can gain an understanding of the features that the model is learning to detect. For example, early layers in the network may detect simple edges and textures, while later layers may detect more complex patterns and shapes.

### Visualization Results

The visualization results are saved in the `results_Bike` and `results_Car` folders, respectively, for Bike and Car images. Each image in these folders represents a feature map for a specific layer and filter.

### Usage

The code for visualizing the feature maps is included in the notebook. You can modify the `layer_name` parameter in the `display_image_filtered` function to visualize feature maps from different layers.

### Observations

By examining the generated visualizations, you might make observations such as:

- **Early layers:** Feature maps in early convolutional layers show simple patterns and textures (edges, corners, blobs).
- **Later layers:** As you go deeper in the network, the feature maps highlight more complex and abstract shapes specific to the dataset (wheels for the bikes, or shapes that define a car, etc.).
- **Importance of individual filters:** Some filters might have strong responses to specific features in the image while others might have weak or general responses. 

These visualizations contribute to the interpretability of the CNN model. By understanding what features activate different filters in different layers, we can gain insights into how the network learns the specific patterns that characterize each class (bikes or cars).

## Usage

To run the project, simply open the notebook in Google Colab and execute the cells in order.

## Acknowledgements

This project is inspired by various tutorials and resources available online.
