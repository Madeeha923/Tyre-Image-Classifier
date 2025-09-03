Tyre Quality Classification using PyTorch
This project explores the classification of digital images of vehicle tyres into 'good' and 'defective' categories using deep learning. Two different approaches were implemented and analyzed using the PyTorch framework:

A Simple Convolutional Neural Network (CNN) built from scratch.

Transfer Learning using a pre-trained ResNet-50 model.

The primary goal was to compare the effectiveness of these two methods and demonstrate key techniques for training and optimizing deep learning models for image classification.

Dataset
The dataset consists of digital images of tyres, organized into two class folders:

/good/: Images of tyres in good condition.

/defective/: Images of tyres with various defects.

A standard split was used to create training and validation sets to properly train and evaluate the models.

Models & Methodology
1. Simple Convolutional Neural Network (CNN)
A basic CNN architecture was designed and trained from scratch. The model consisted of several convolutional blocks followed by fully connected layers for classification.

Key Techniques:

Data Preprocessing: Images were resized to a uniform size (e.g., 128x128) and normalized.

Standard Training Loop: The model was trained for a set number of epochs using an Adam optimizer and Cross-Entropy Loss.

2. Transfer Learning with ResNet-50
To leverage the power of pre-trained models, a ResNet-50 architecture, pre-trained on the large-scale ImageNet dataset, was adapted for this task. The final classification layer of the ResNet-50 was replaced with a new layer suited for our binary classification problem.

Key Techniques:

Fine-Tuning: Initially, only the weights of the new classification layer were trained. Subsequently, more layers of the network can be "unfrozen" and trained with a lower learning rate.

Data Augmentation: To prevent overfitting and improve generalization, the training dataset was augmented with random transformations such as horizontal flips, rotations, and color jitter.

Early Stopping: A crucial technique was implemented to monitor the validation loss. The training process was automatically halted when the validation loss stopped improving for a set number of "patience" epochs. This ensures that the model with the best generalization performance is saved.

Results & Analysis
The performance of the two models was drastically different, highlighting the common challenges and solutions in deep learning.

Simple CNN Results
The simple CNN showed classic signs of overfitting after only a few epochs:

Epoch

Train Loss

Val Loss

Val Accuracy

1

0.7100

0.6283

0.6388

2

0.5345

0.5810

0.6981

3

0.4313

0.5746

0.7385

4

0.3024

0.7446

0.6954

5

0.2126

1.2756

0.6496

Analysis:

The model's performance peaked at Epoch 3, achieving ~74% validation accuracy.

After this point, the training loss continued to decrease, but the validation loss spiked dramatically. This divergence is a clear indicator that the model was memorizing the training data instead of learning general features.

Transfer Learning (ResNet-50) Results
The transfer learning approach yielded significantly better and more stable results, effectively managed by early stopping:

Epoch

Train Loss

Val Loss

Val Acc

Notes

1

0.3069

0.4563

0.9110



2

0.2882

0.3234

0.9164

 Loss improved

3

0.2708

0.3079

0.9245

 Loss improved

4

0.2557

0.2790

0.9029

 Best Model Saved

5

0.2513

0.5753

0.9299

 No improvement (Counter 1/3)

6

0.2275

0.3750

0.9299

 No improvement (Counter 2/3)

7

0.1898

0.4069

0.9272

 Early Stopping Triggered

Analysis:

The transfer learning model achieved a much higher validation accuracy, peaking above 92%.

Early stopping successfully identified that the model's best performance was at Epoch 4 and stopped the training at Epoch 7, preventing the model from degrading due to overfitting.

