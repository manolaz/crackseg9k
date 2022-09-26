# Pix2Pix U-Net (Without Features)

### Introduction
This is a Tensorflow(2.8.2) implementation of the image-to-image translation model - Pix2Pix with a U-Net backbone, on the crackseg9k dataset.

### Set-up:
The code was tested with Anaconda and Python 3.6. After installing the Anaconda environment:

0. Clone the repo:
    ```Shell
    git clone https://github.com/Dhananjay42/crackseg9k.git
    cd crackseg9k/pix2pix/without_features
    ```

1. Install dependencies:

    ```Shell
    pip install -r requirements
    ```

2. Set-Up: To get the code running, you will need to structure your data a certain file. Download the crackseg9k dataset available here, and copy it into a folder. Your folder should be structured like this:

### Folder Structure for Training
    .
    ├── Images                  # Contains the RGB images.
    ├── Masks                   # Contains the corresponding segmentation masks. 
    ├── progress                # Predictions are saved in this folder after each epoch, to monitor the model training. (Note: only required for training)
    ├── logs                    # The loss curves are stored here - also, to monitor the training process. (Note: only required for training) 
    ├── train.txt               # This can be obtained from the dataset. This is a list of the names of all the training images, on separate lines. 
    ├── test.txt                # This can also be obtained from the dataset. This is a list of the names of all the testing images, on separate lines. 

Note: You are free to make your own train.txt and test.txt files. We have made them by considering an even split of each sub-dataset between the train and test folders. 

### Training
Follow the steps below to train your model:

0. Configure your dataset to the folder structure shown above. 

1. Input arguments: (see full input arguments via python train.py --help):
    ```Shell
    usage: train.py [-h] [--input_dir <link to your directory>]
                [--checkpoint_dir <link to your checkpoint folder>] [--batch_size BATCH_SIZE]
                [--lambda LAMBDA] [--epochs EPOCHS] [--buffer_size BUFFER_SIZE]

    ```
    You can keep track of the training process by monitoring the "progress" and the "logs" folders. The "progress" folder shows a random test image, the ground truth, and the predicted mask as a function of the number of epochs. The "logs" folder stores the file to monitor training. 

### Inferencing using the trained model

0. For this, you just need a folder with RGB images. You can either have inferences on all of them, or you can specify which files you want to run inferences on using the "test.txt" file. 

1. To get inferences from a trained model, do:
    ```Shell
    usage: inference.py [-h] [--input_dir <link to folder with images>] 
           [--output_dir <link to folder to store predictions in>] 
           [--checkpoint_dir <link to folder with checkpoints>]
           [--options {1,2}]
  
    ```
    By selecting the option-1, you will have to specify a "test.txt" file name, with names of the images separated by lines.
    
    By selecting the option-2, you don't need this .txt file, and the inferencing is done on all images in the input folder. 

### Evaluating the trained model 

0. For this, you will need to have the following folder structure:
   
### Folder Structure for Evaluation
    .
    ├── Images                  # Contains the RGB images.
    ├── Masks                   # Contains the corresponding segmentation masks. 
    ├── test.txt                # This can also be obtained from the dataset. This is a list of the names of all the testing images, on separate lines. (This is optional).

1. To evaluate the trained pix2pix model on a dataset:
    ```Shell
    usage: evaluate.py [-h] [--input_dir <link to folder with images>] 
           [--checkpoint_dir <link to folder with checkpoints>]
           [--options {1,2}]
    ```
    
    By selecting the option-1, you will have to specify a "test.txt" file name, with names of the images separated by lines.
    
    By selecting the option-2, you don't need this .txt file, and the inferencing is done on all images in the input folder. 
    
### Acknowledgement
[pix2pix](https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/generative/pix2pix.ipynb)