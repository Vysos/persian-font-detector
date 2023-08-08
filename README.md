## Persian Font Detection

This project trains a deep convolutional neural network to detect 16 famous Persian fonts in images. The model can accurately recognize the font of Persian text in an image.

### Dataset

Click [here](https://github.com/Vysos/persian-font-detector/blob/main/Dataset/README.md) to see a detailed description of the used dataset.

### Model Architecture

The model uses a ResNet-101 architecture pre-trained on ImageNet. The convolutational layers are frozen and the fully connected layer is replaced with a new one matching the number of classes (16).

This transfer learning approach allows the model to leverage features learned on large datasets like ImageNet. The model only has to learn the new classification layer.

The replaced fully connected layer uses a LogSoftmax activation for multi-class prediction.

The model is trained for 5 epochs with cross-entropy loss, SGD optimizer with 0.001 learning rate and 0.9 momentum. A StepLR scheduler reduces the LR by 10x every 7 epochs.

Data is augmented on-the-fly with random horizontal flips. Images are resized to 224x224, normalized, and batched with 4 images per batch.

### Usage

The `ResNet101_Torch.ipynb` notebook contains the full code to:

- Load and preprocess the images
- Define, train and evaluate the ResNet model
- Make predictions on new images


To use the model:

Download the trained model from [here](https://drive.google.com/file/d/18CO6XBws-9B12jS1h8eslGB-qMeCeB8I/view?usp=drive_link).

```python
model = torch.load('Trained_ResNet101.pth')
model.eval() 

# Load image, preprocess, normalize 
img = preprocess(image_path)  

# Make prediction
pred = model(img)
font_class = class_names[pred.argmax()] 
```

### Results

The model achieves:

- 99.9% test accuracy after 5 epochs of training 
- 99.91% best validation accuracy

This demonstrates it can accurately detect the 16 Persian fonts with high precision.

The training logs, predictions, and examples are shown in the notebook.

### Future Work

Some ideas for extending this project:

- Add more fonts and images to recognize more classes
- Try different model architectures like ResNet-50, DenseNet, etc.
- Deploy the model on a web app for public use
- Optimize the model for mobile devices
