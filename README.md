# Tyre Quality Classification using PyTorch  

This project explores the classification of digital images of vehicle tyres into **'good'** and **'defective'** categories using deep learning.  
Two different approaches were implemented and analyzed using the **PyTorch** framework:

1. **A Simple Convolutional Neural Network (CNN)** built from scratch  
2. **Transfer Learning** using a pre-trained **ResNet-50** model  

The primary goal was to compare the effectiveness of these two methods and demonstrate key techniques for training and optimizing deep learning models for image classification.  

---

##  Dataset  

The dataset consists of digital images of tyres, organized into two class folders:  

- `/good/` → Images of tyres in good condition  
- `/defective/` → Images of tyres with various defects  

A standard train/validation split was used for proper training and evaluation.  

---

## Models & Methodology  

###  Simple Convolutional Neural Network (CNN)  
A basic CNN architecture was designed and trained from scratch. The model consisted of several convolutional blocks followed by fully connected layers for classification.  

**Key Techniques:**  
- **Data Preprocessing:** Images resized  and normalized  
- **Training Loop:** Adam optimizer + Cross-Entropy Loss  

---

###  Transfer Learning with ResNet-50  
A **ResNet-50** model pre-trained on **ImageNet** was adapted for binary classification.  

**Key Techniques:**  
- **Fine-Tuning:** Started with only the new classification layer → gradually unfroze more layers with a lower LR  
- **Data Augmentation:** Horizontal flips, rotations, color jitter  
- **Early Stopping:** Training stopped when validation loss stopped improving  

---

##  Results & Analysis  

###  Simple CNN Results  
The simple CNN showed **overfitting** after only a few epochs.  

| Epoch | Train Loss | Val Loss | Val Accuracy |
|-------|-----------:|---------:|-------------:|
| 1     | 0.7100     | 0.6283   | 0.6388       |
| 2     | 0.5345     | 0.5810   | 0.6981       |
| 3     | 0.4313     | 0.5746   | 0.7385       |
| 4     | 0.3024     | 0.7446   | 0.6954       |
| 5     | 0.2126     | 1.2756   | 0.6496       |

**Analysis:**  
- Best performance: **~74% validation accuracy (Epoch 3)**  
- After that, validation loss increased while training loss decreased → **classic overfitting**  

---

###  Transfer Learning (ResNet-50) Results  
Transfer learning yielded **much better and stable results**, with **early stopping** preventing overfitting.  

| Epoch | Train Loss | Val Loss | Val Accuracy | Notes                 |
|-------|-----------:|---------:|-------------:|-----------------------|
| 1     | 0.3069     | 0.4563   | 0.9110       |                       |
| 2     | 0.2882     | 0.3234   | 0.9164       | Loss improved         |
| 3     | 0.2708     | 0.3079   | 0.9245       | Loss improved         |
| 4     | 0.2557     | 0.2790   | 0.9029       | Best model saved   |
| 5     | 0.2513     | 0.5753   | 0.9299       | No improvement (1/3)  |
| 6     | 0.2275     | 0.3750   | 0.9299       | No improvement (2/3)  |
| 7     | 0.1898     | 0.4069   | 0.9272       | ⏹ Early Stopping     |

**Analysis:**  
- Achieved **>92% validation accuracy**  
- Best model saved at **Epoch 4**  
- Early stopping prevented overfitting and preserved generalization  

---

##  Conclusion  

This project effectively demonstrates the power of transfer learning. The pre-trained ResNet-50 model yielded a more accurate and stable result, in stark contrast to the simple CNN, showcasing a clear advantage for leveraging established architectures in image classification.  

