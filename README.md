# Efficient Noise Reduction and HOG Feature Extraction for Sign Language Recognition

MATLAB implementation of the research paper **“Efficient Noise Reduction and HOG Feature Extraction for Sign Language Recognition”**, presented at the **2018 International Conference on Advancement in Electrical and Electronic Engineering (ICAEEE 2018)**.

The project implements an image-based **American Sign Language (ASL) alphabet recognition** system using image preprocessing, hand segmentation, Canny edge detection, **Histogram of Oriented Gradients (HOG)** feature extraction, and a **K-Nearest Neighbors (KNN)** classifier.

The proposed approach achieved **94.23% classification accuracy** on the reported test set, outperforming the Bag-of-Features + SVM comparison method, which achieved **86%**.

---

## 📄 Research Paper

**Efficient Noise Reduction and HOG Feature Extraction for Sign Language Recognition**

**Authors**

* Iqbal Mahmud
* Tasnim Tabassum
* Md. Palash Uddin
* Emran Ali
* Adiba Mahjabin Nitu
* Masud Ibn Afjal

Published at **ICAEEE 2018**, Gazipur, Bangladesh.

**DOI:** [10.1109/ICAEEE.2018.8642983](https://doi.org/10.1109/ICAEEE.2018.8642983)

* [ResearchGate – Full Paper](https://www.researchgate.net/publication/330924607_Efficient_Noise_Reduction_and_HOG_Feature_Extraction_for_Sign_Language_Recognition)
* [IEEE Xplore](https://ieeexplore.ieee.org/document/8642983)

---

## 🔍 Overview

Automatic sign language recognition is a computer vision problem where visual hand signs are classified into their corresponding characters.

This project follows the approach proposed in the paper:

```text
Input Image
     │
     ▼
Logarithmic Transformation
     │
     ▼
Histogram Equalization
     │
     ▼
L*a*b Color-Space Segmentation
     │
     ▼
Binary Image
     │
     ▼
Canny Edge Detection
     │
     ▼
HOG Feature Extraction
     │
     ▼
KNN Classifier
     │
     ▼
Recognized ASL Character
```

The preprocessing stage is designed to reduce background noise and isolate the hand before extracting shape-based HOG features.

---

## 🧠 Method

### 1. Image Preprocessing

The input images are enhanced using image-processing operations described in the paper.

#### Logarithmic Transformation

A logarithmic transformation is applied to improve image intensity distribution and enhance relevant visual information.

#### Histogram Equalization

Histogram equalization is then used to improve contrast and stretch the available intensity range.

---

### 2. Hand Segmentation

The hand is separated from the background using **L*a*b color-space segmentation**.

The repository includes an implementation generated using MATLAB's Image Segmenter workflow in:

```text
SegmentImage.m
```

This produces a binary/masked representation of the hand region, reducing the influence of background objects.

---

### 3. Canny Edge Detection

After segmentation, the image is converted into a binary representation and edge information is extracted using the **Canny edge detector**.

The resulting edges provide the structural information needed for shape-based feature extraction.

---

### 4. HOG Feature Extraction

The proposed method uses **Histogram of Oriented Gradients (HOG)** to describe the shape and edge structure of each sign.

The main implementation is:

```text
ASLRecognitionWithHOGFeaturesAndKNNClassifier.m
```

The implementation uses MATLAB's `extractHOGFeatures()` function and stores the resulting feature vectors in a training feature matrix.

---

### 5. KNN Classification

The extracted HOG features are classified using a multi-class **K-Nearest Neighbors (KNN)** classifier.

The classifier is created using MATLAB's:

```matlab
fitcknn()
```

The system recognizes all **26 English alphabet characters (A–Z)**.

---

## 📊 Dataset

The experiment described in the paper uses an American Sign Language alphabet dataset containing:

* **26 classes:** A–Z
* **572 total images**
* **22 images per character**
* **200 × 200 × 3** RGB images
* **65% training / 35% testing split**
* **14 training images per character**
* **8 testing images per character**

The repository expects the image dataset to be organized into MATLAB `imageSet`-compatible class directories.

> **Note:** The dataset itself is not included in this repository.

---

## 📈 Results

The paper reports the following overall result on the test set:

| Method              | Classifier            | Test Accuracy |
| ------------------- | --------------------- | ------------: |
| **Proposed Method** | **HOG + KNN**         |    **94.23%** |
| Comparison Method   | Bag of Features + SVM |    **86.00%** |

The proposed method correctly classified **196 out of 208 test samples**.

### Per-class results

| Character | Accuracy |
| --------- | -------: |
| A         |     100% |
| B         |     100% |
| C         |     100% |
| D         |     100% |
| E         |     100% |
| F         |     100% |
| G         |     100% |
| H         |     100% |
| I         |     100% |
| J         |     100% |
| K         |     100% |
| L         |    87.5% |
| M         |     100% |
| N         |     100% |
| O         |      75% |
| P         |     100% |
| Q         |     100% |
| R         |     100% |
| S         |      50% |
| T         |     100% |
| U         |     100% |
| V         |      75% |
| W         |     100% |
| X         |    87.5% |
| Y         |     100% |
| Z         |      75% |

---

## 🆚 Comparison Method

For comparison, the project also includes a **Bag-of-Features** implementation:

```text
ASLRecognitionWithBagOfFeatures.m
```

This approach uses MATLAB's Bag-of-Features pipeline and an image category classifier.

The implementation:

1. Loads the training and test sets
2. Builds a Bag-of-Features representation
3. Trains an image category classifier
4. Predicts the test set
5. Generates a confusion matrix

The paper reports **86% test accuracy** for this comparison approach.

---

## 📁 Repository Structure

```text
.
├── TrainingMatrix/
│
├── ASLRecognitionWithHOGFeaturesAndKNNClassifier.m
├── ASLRecognitionWithBagOfFeatures.m
├── GenarateConfusionMatrix.m
├── PlotConfusion.m
├── SegmentImage.m
├── batchmyimfcn.m
├── myimfcn.m
│
└── LICENSE
```

### Main files

| File                                              | Description                                                 |
| ------------------------------------------------- | ----------------------------------------------------------- |
| `ASLRecognitionWithHOGFeaturesAndKNNClassifier.m` | Main HOG feature extraction and KNN classification pipeline |
| `ASLRecognitionWithBagOfFeatures.m`               | Bag-of-Features comparison implementation                   |
| `SegmentImage.m`                                  | Hand/background segmentation function                       |
| `GenarateConfusionMatrix.m`                       | Generates classification confusion matrix                   |
| `PlotConfusion.m`                                 | Visualization of confusion matrix                           |
| `myimfcn.m`                                       | Image processing function                                   |
| `batchmyimfcn.m`                                  | Batch image processing                                      |
| `TrainingMatrix/`                                 | Training-related data/matrices                              |

---

## 🛠️ Requirements

The implementation is written in **MATLAB** and uses functionality from MATLAB's computer vision/image processing ecosystem.

Recommended:

* MATLAB
* Image Processing Toolbox
* Computer Vision Toolbox
* Classification / Statistics and Machine Learning functionality

The exact toolbox requirements may vary depending on the MATLAB release being used.

---

## 🚀 Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/zero-jim/Efficient-Noise-Reduction-and-HOG-Feature-Extraction-for-Sign-Language-Recognition.git

cd Efficient-Noise-Reduction-and-HOG-Feature-Extraction-for-Sign-Language-Recognition
```

### 2. Prepare the dataset

Place the ASL dataset in the expected directory structure.

The main HOG implementation loads the dataset using:

```matlab
handDatabase = imageSet('DataATT','recursive');
```

Therefore, the dataset should be available under:

```text
DataATT/
├── A/
├── B/
├── C/
├── ...
└── Z/
```

Each directory should contain the corresponding character images.

### 3. Run the HOG + KNN implementation

Open:

```text
ASLRecognitionWithHOGFeaturesAndKNNClassifier.m
```

and run the script from MATLAB.

The script:

* Creates the image database
* Splits the data into training and testing sets
* Extracts HOG features
* Trains the KNN classifier
* Predicts test images
* Displays the recognized sign

The repository implementation uses a **65:35 training/testing split**, consistent with the experimental setup described in the paper.

---

## 🧪 Reproducing the Paper

To reproduce the main experiment:

1. Obtain the ASL alphabet dataset used in the paper.
2. Arrange the images into the expected class-directory structure.
3. Run the preprocessing/segmentation pipeline.
4. Run `ASLRecognitionWithHOGFeaturesAndKNNClassifier.m`.
5. Generate the confusion matrix using the provided scripts.
6. Compare the result with `ASLRecognitionWithBagOfFeatures.m`.

The published experiment used 364 training samples and 208 testing samples, with 196 of the 208 test samples correctly recognized by the proposed method.

---

## 📚 Citation

If you use this implementation or the underlying research, please cite the original paper:

```bibtex
@inproceedings{mahmud2018efficient,
  title={Efficient Noise Reduction and HOG Feature Extraction for Sign Language Recognition},
  author={Mahmud, Iqbal and Tabassum, Tasnim and Uddin, Md. Palash and Ali, Emran and Nitu, Adiba Mahjabin and Afjal, Masud Ibn},
  booktitle={2018 International Conference on Advancement in Electrical and Electronic Engineering (ICAEEE)},
  year={2018},
  doi={10.1109/ICAEEE.2018.8642983}
}
```

---

## 📜 License

This repository is released under the **Apache License 2.0**.

See [`LICENSE`](./LICENSE) for the complete license text.

---

## 🔗 References

* **Repository:** https://github.com/zero-jim/Efficient-Noise-Reduction-and-HOG-Feature-Extraction-for-Sign-Language-Recognition
* **Research paper:** https://www.researchgate.net/publication/330924607_Efficient_Noise_Reduction_and_HOG_Feature_Extraction_for_Sign_Language_Recognition
* **IEEE Xplore:** https://ieeexplore.ieee.org/document/8642983
* **DOI:** https://doi.org/10.1109/ICAEEE.2018.8642983

---

## 🙏 Acknowledgment

This repository contains the code associated with the research paper **“Efficient Noise Reduction and HOG Feature Extraction for Sign Language Recognition.”**

The implementation is intended to facilitate reproducibility and provide a practical reference for classical computer-vision-based sign language recognition using image preprocessing, HOG features, and KNN classification.
