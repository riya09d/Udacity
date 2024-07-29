## UDACITY - NANODEGREE PROJECT
# Use a Pre-trained Image Classifier to Identify Dog Breeds

To address the requirements for your project on identifying dog breeds using a pre-trained image classifier, you’ll need to ensure that several criteria are met. Below is a structured approach to fulfill each requirement, including code examples and explanations.

### Project Overview

**Objective**: Use a pre-trained image classifier to identify dog breeds and time the code execution. Handle command-line arguments for input directories, model architectures, and dog breed files.

### 1. Timing Code Execution

To measure the time taken by your code, use Python's `time` module.

**Implementation**:

```python
import time

def main():
    start_time = time.time()
    
    # Main logic here
    classify_images(images_dir, results_dic, model)
    
    end_time = time.time()
    elapsed_time = end_time - start_time
    print(f"Elapsed time: {elapsed_time:.2f} seconds")
```

### 2. Command-Line Arguments

You need to handle command-line arguments to specify the directory, model architecture, and dog breed file. Use the `argparse` module for this.

**Implementation**:

```python
import argparse

def parse_args():
    parser = argparse.ArgumentParser(description='Image classification arguments.')
    parser.add_argument('--dir', type=str, default='pet_images/', help='Directory of images.')
    parser.add_argument('--arch', type=str, default='vgg', help='Pre-trained model architecture.')
    parser.add_argument('--dogfile', type=str, default='dognames.txt', help='File containing dog breed names.')
    return parser.parse_args()

if __name__ == '__main__':
    args = parse_args()
    images_dir = args.dir
    model = args.arch
    dogfile = args.dogfile
    # Continue with the rest of your code
```

### 3. Pet Image Labels

Ensure the dictionary format for pet image labels is correct and contains 40 key-value pairs.

**Example**:

```python
def get_pet_labels(image_dir):
    # Implement logic to retrieve pet labels
    results_dic = {
        'Poodle_07956.jpg': ['poodle'],
        'fox_squirrel_01.jpg': ['fox squirrel'],
        # Ensure to have 40 pairs
    }
    return results_dic
```

### 4. Classifying Images

Make sure to append the image directory to each filename before calling the classifier function. Also, handle output formatting correctly.

**Implementation**:

```python
def classify_images(images_dir, results_dic, model):
    for key in results_dic:
        image_path = images_dir + key
        classifier_label = classifier(image_path, model)
        classifier_label = classifier_label.lower().strip()
        
        if results_dic[key][0] in classifier_label:
            results_dic[key].extend([classifier_label, 1])
        else:
            results_dic[key].extend([classifier_label, 0])
```

### 5. Classifying Labels as Dogs

Verify that classifier labels are correctly classified as "dogs" or "not dogs."

**Implementation**:

```python
def classify_dogs(results_dic):
    for key, value in results_dic.items():
        pet_label, classifier_label, match_status = value
        if 'dog' in pet_label:
            if 'dog' in classifier_label:
                print(f"{key}: Correctly identified as dog")
            else:
                print(f"{key}: Incorrectly identified as not a dog")
        else:
            if 'dog' not in classifier_label:
                print(f"{key}: Correctly identified as not a dog")
            else:
                print(f"{key}: Incorrectly identified as a dog")
```

### 6. Results

Ensure accurate scoring of models by running a batch script.

**Implementation**:

1. Write a shell script `run_models_batch.sh`:

    ```bash
    #!/bin/bash
    python main.py --dir pet_images/ --arch vgg --dogfile dognames.txt
    python main.py --dir pet_images/ --arch resnet --dogfile dognames.txt
    python main.py --dir pet_images/ --arch alexnet --dogfile dognames.txt
    ```

2. Execute the script and verify the output.

    ```bash
    chmod +x run_models_batch.sh
    ./run_models_batch.sh
    ```

### README

Here’s a README file summarizing the project:

```markdown
#  Image Classifier to Identify Dog Breeds.

## Overview

This project utilizes pre-trained CNN models to classify images of dogs into breeds. It includes timing of code execution, command-line argument handling, and accurate classification of dog breeds.

## Features

- **Image Classification**: Classify images using models like VGG, ResNet, and AlexNet.
- **Timing**: Measure and display the time taken for classification.
- **Command-Line Arguments**: Customize image directory, model architecture, and dog breed file.
- **Results Formatting**: Proper formatting and classification of results.

## Prerequisites

- Python 3.x
- Required Python packages listed in `requirements.txt`

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/image-classification-project.git
   cd image-classification-project
   ```

2. **Install Required Packages**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   pip install -r requirements.txt
   ```

## Usage

1. **Run the Project**

   ```bash
   python main.py --dir pet_images/ --arch vgg --dogfile dognames.txt
   ```

2. **Batch Processing**

   Execute the batch script to run multiple models:

   ```bash
   chmod +x run_models_batch.sh
   ./run_models_batch.sh
   ```

## Results

- **Timing**: Check the elapsed time for each model run.
- **Classification**: Review the output for accuracy in identifying dog breeds.

## Contributing

Contributions are welcome. Please fork the repository and submit pull requests with your enhancements or fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

