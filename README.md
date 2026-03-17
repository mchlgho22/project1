# Face Recognition Gender Classification using GoogLeNet

Proyek ini merupakan implementasi Face Recognition untuk klasifikasi gender (Male / Female) menggunakan arsitektur Deep Learning berbasis GoogLeNet dengan framework PyTorch.
Model dilatih menggunakan dataset wajah dari CelebFaces Attributes Dataset dan memanfaatkan teknik transfer learning dari model pretrained ImageNet.

## Project Overview

Tujuan proyek ini adalah membangun model computer vision yang mampu:
 - Mendeteksi wajah dari dataset gambar
 - Mengklasifikasikan gender:
   - Male
   - Female

## Dataset

Dataset yang digunakan berasal dari: CelebFaces Attributes Dataset (CelebA)

Dataset berisi:
 - lebih dari 200.000 gambar wajah
 - 40 atribut waja

Pada proyek ini hanya digunakan atribut:
 - Male

Dataset kemudian diubah menjadi label:
 - 1  Male	
 - 0  Female	

Jumlah data yang digunakan:
 - 5000 gambar wajah
 - diambil secara random sampling

Distribusi data contoh:
  | Gender        | Jumlah            |
  | ------------- | ----------------- |
  | Male          | 2047              |
  | Female Size   | 2953              |

## Data Preparation

Dataset dibagi menggunakan Stratified Split agar distribusi gender tetap seimbang.
 - Train set: 80%
 - Test set: 20%

## Dataset Structure

Dataset link download : <a href="https://drive.google.com/drive/folders/1mMuXkAFu4IHOq8-p0Kr7zwhsVkW-0Kqj?usp=sharing" download>Google Drive</a>
<ul>
    <li>Dataset
        <ul>
            <li>Images
                <ul>
                    <li class="file">000001.jpg</li>
                    <li class="file">000002.jpg</li>
                    <li class="file">...</li>
                </ul>
            </li>
            <li class="file">list_attribute.txt</li>
            <li>model_saved</li>
        </ul>
    </li>
</ul>
  
## Data Preprocessing

Sebelum masuk ke model, gambar dilakukan preprocessing menggunakan Torchvision Transform:

**Training Transform**
 - Resize 224x224
 - Random Horizontal Flip
 - Random Rotation
 - Color Jitter
 - Normalization (ImageNet)
 - Testing Transform
 - Resize 224x224
 - Normalization

Contoh transform:
 - Resize(224,224) 
 - RandomHorizontalFlip() 
 - RandomRotation(10) 
 - ColorJitter() 
 - Normalize(ImageNet mean/std)

## Model Architecture

Model yang digunakan adalah GoogLeNet (Inception v1) dengan transfer learning.

Langkah yang dilakukan:
  1. Load pretrained model ImageNet
  2. Freeze sebagian besar layer
  3. Unfreeze layer lebih dalam:
      - inception4
      - inception5
  4. Mengganti classifier terakhir menjadi:
     Fully Connected Layer
     Output: 2 classes (Male, Female)

Optimizer yang digunakan:
  - Adam
  - learning rate berbeda untuk setiap layer

Loss Function: CrossEntropyLoss <br>
Learning rate scheduler: ReduceLROnPlateau

## Training Configuration
Parameter training:
  | Parameter     | Value             |
  | ------------- | ----------------- |
  | Epoch         | 10                |
  | Batch Size    | 32                |
  | Optimizer     | Adam              |
  | Loss Function | CrossEntropyLoss  |
  | Scheduler     | ReduceLROnPlateau |
  
Model terbaik akan disimpan pada: model_saved/best_model.pth

## Training Visualization

Selama training, sistem mencatat:
  - Train Loss
  - Test Loss
  - Train Accuracy
  - Test Accuracy

Kemudian divisualisasikan dalam grafik:
  - Loss per Epoch
  - Accuracy per Epoch

**Model Evaluation**

Evaluasi model dilakukan menggunakan:
  - Classification Report
  - Confusion Matrix

Metode evaluasi menggunakan library:
  - sklearn
  - seaborn
  - matplotlib

Output evaluasi:
  - Precision
  - Recall
  - F1-score
  - Support

## Prediction Visualization
Model juga menampilkan hasil prediksi pada beberapa gambar test.

Informasi yang ditampilkan:
  - Gambar wajah
  - Label asli
  - Label prediksi
  - Confidence score

## Project Structure

<ul>
    <li>Dataset
        <ul>
            <li>FaceRecognition
                <ul>
                    <li class="file">Images/</li>
                    <li class="file">list_attribute.txt</li>
                    <li class="file">model_saved/</li>
                </ul>
            </li>
        </ul>
    </li>
</ul>
    
## Requirements
Library yang digunakan:
 - torch
 - torchvision
 - pandas
 - numpy
 - scikit-learn
 - matplotlib
 - seaborn
 - Pillow





