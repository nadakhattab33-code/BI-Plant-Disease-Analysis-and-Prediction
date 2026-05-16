# Business Intelligence System for Plant Disease Analysis and Prediction

## Project Overview

This graduation project presents a Business Intelligence system for plant disease analysis and prediction. The system combines a deep learning image classification model with an interactive Power BI dashboard to analyze model performance and visualize prediction results.

The project focuses on classifying plant leaf images into healthy and diseased classes using transfer learning with EfficientNetB0. The model evaluation results were exported and used to build a Power BI dashboard that supports performance analysis, class-level comparison, and confusion matrix visualization.

---

## Objectives

The main objectives of this project are:

- Build a deep learning model for plant disease classification.
- Classify plant leaf images into healthy or diseased categories.
- Predict the specific plant disease class.
- Evaluate the model using multiple performance metrics.
- Analyze class-level model performance.
- Visualize results using a Power BI dashboard.
- Support decision-making through a Business Intelligence reporting system.

---

## Dataset Summary

The dataset contains plant leaf images organized into class folders. Each folder represents either a healthy plant class or a specific plant disease class.

Dataset summary:

- Number of classes: 38
- Training images: 34,765
- Validation images: 8,691
- Test images: 10,845

![Dataset Size](images/dataset_size.png)

---
## Dataset Link

The dataset file is too large to upload directly to GitHub.  
It is available through OneDrive:

[Download Dataset](https://1drv.ms/u/c/cd9639f1b9c7cd16/IQDAC8WoyGhfTZWUKBS5cJvcARViLL-QPLm5tK4ovO6VB-I?e=kNnuw0)

## Dataset Samples

The following image shows samples from the plant leaf dataset. The dataset includes multiple plant types and disease categories, such as tomato diseases, potato diseases, apple diseases, corn diseases, grape diseases, and healthy plant leaves.

![Dataset Samples](images/dataset_samples.png)

---

## Class Distribution

The training image distribution was visualized to check whether the dataset is balanced across all classes.

![Class Distribution](images/class_distribution.png)

The chart shows that the dataset contains class imbalance, where some classes have more images than others. Because of this, the project does not rely only on accuracy. Instead, multiple metrics were used to evaluate the model more fairly, including:

- Accuracy
- Macro F1-score
- Weighted F1-score
- Balanced Accuracy
- Confusion Matrix

---

## Data Quality and Data Leakage Check

Before training the model, the dataset was checked for corrupted images and duplicate images between the training and test sets.

The data quality check showed:

- Corrupted training images: 0
- Corrupted test images: 0
- Exact duplicate test images found: 4
- Duplicate test images removed: 4
- Final duplicate count after re-checking: 0

This step is important because duplicate images between training and testing data can cause data leakage. Data leakage may make the model accuracy appear higher than it really is. Removing duplicate test images helps ensure a more reliable final evaluation.

![Duplicate Check](images/duplicate_check.png)

---

## Model Architecture

The model uses transfer learning with EfficientNetB0 as the backbone model.

EfficientNetB0 was selected because it is a strong pretrained convolutional neural network that performs well on image classification tasks while being efficient in terms of parameters and computation.

The model architecture includes:

- Data Augmentation layer
- EfficientNetB0 pretrained feature extractor
- GlobalAveragePooling2D
- BatchNormalization
- Dropout
- Dense layer
- Final Softmax output layer with 38 neurons

The final output layer contains 38 neurons because the dataset contains 38 plant disease and healthy classes.

![Model Summary](images/model_summary.png)

---

## Transfer Learning Approach

The project uses transfer learning instead of training a CNN model from scratch.

Transfer learning was used because:

- It improves model performance on image classification tasks.
- It reduces training time.
- It works well when using pretrained knowledge from ImageNet.
- It helps the model learn useful visual features such as edges, textures, shapes, and patterns.

The training process was divided into two stages:

### Stage 1: Classification Head Training

In the first stage, the EfficientNetB0 base model was frozen, and only the custom classification head was trained.

This allows the new layers to learn how to classify the plant disease classes without changing the pretrained feature extractor.

### Stage 2: Fine-Tuning

In the second stage, some of the final layers of EfficientNetB0 were unfrozen and trained using a smaller learning rate.

Fine-tuning helps improve the model by allowing the pretrained model to adapt more specifically to plant leaf disease images.

---

## Training Configuration

The model was trained using the following configuration:

- Backbone model: EfficientNetB0
- Image size: 160 × 160
- Number of classes: 38
- Loss function: Sparse Categorical Crossentropy
- Optimizer: Adam
- Evaluation metrics: Accuracy and Top-3 Accuracy

Callbacks used during training:

- EarlyStopping
- ReduceLROnPlateau
- ModelCheckpoint

Due to Google Colab free runtime limitations, full model retraining may require sufficient GPU and RAM resources. Therefore, this repository also includes saved outputs from a successful run, including the classification report, confusion matrices, model metadata, training history, and Power BI dashboard screenshots.

---

## Model Evaluation

The model was evaluated on a separate test set that was not used during training.

The evaluation process included:

- Overall accuracy
- Macro F1-score
- Weighted F1-score
- Balanced accuracy
- Class-level precision
- Class-level recall
- Class-level F1-score
- Confusion matrix
- Normalized confusion matrix

![Power BI Overview](images/powerbi_overview.png)

---

## Class Performance Analysis

The Power BI dashboard includes class-level performance analysis. This helps identify which plant disease classes are classified well and which classes may be more difficult for the model.

The class performance page includes:

- F1-score per class
- Precision comparison
- Recall comparison
- Disease-wise evaluation

![Class Performance](images/class_performance.png)

---

## Confusion Matrix

A normalized confusion matrix was used to analyze the classification performance across all classes.

The confusion matrix helps show:

- Correctly classified classes
- Misclassified classes
- Similar disease categories that may be confused by the model
- Overall classification behavior across the 38 classes

![Confusion Matrix](images/confusion_matrix_dashboard.png)

---

## Model Pipeline

The project follows an end-to-end workflow starting from dataset preparation, model training, model evaluation, and finally visualizing the results using Power BI.

![Model Pipeline](images/model_pipeline.png)

---

## Power BI Dashboard

The Power BI dashboard was created to visualize and analyze the CNN model evaluation results.

The dashboard includes:

- Project overview
- Model pipeline
- Model performance metrics
- Class performance analysis
- Confusion matrix heatmap
- Model conclusion

The dashboard uses exported model result files, including:

- `classification_report.csv`
- `confusion_matrix.csv`
- `normalized_confusion_matrix.csv`
- `training_history.json`
- `model_metadata.json`
- `class_names.json`

The full Power BI dashboard file is available in this repository:

`project.pbix`

---

## Project Files

| File | Description |
|---|---|
| `plant_disease_analysis_prediction_notebook.ipynb` | Main Colab notebook containing the model code |
| `class_names.json` | List of the 38 plant disease and healthy classes |
| `classification_report.csv` | Precision, recall, F1-score, and support for each class |
| `confusion_matrix.csv` | Confusion matrix values |
| `normalized_confusion_matrix.csv` | Normalized confusion matrix values |
| `model_metadata.json` | Model configuration and metadata |
| `training_history.json` | Training and validation accuracy/loss history |
| `project.pbix` | Power BI dashboard file |
| `dataset_size.png` | Dataset summary screenshot |
| `dataset_samples.png` | Dataset sample images screenshot |
| `class_distribution.png` | Training images per class chart |
| `duplicate_check.png` | Data quality and duplicate check screenshot |
| `model_summary.png` | Model architecture summary screenshot |
| `powerbi_overview.png` | Power BI overview dashboard screenshot |
| `class_performance.png` | Class performance dashboard screenshot |
| `confusion_matrix_dashboard.png` | Power BI confusion matrix screenshot |
| `model_pipeline.png` | Model pipeline dashboard screenshot |

---

## Technologies Used

The project uses the following tools and technologies:

- Python
- Google Colab
- TensorFlow
- Keras
- EfficientNetB0
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- Power BI
- GitHub

---

## Challenges

Some challenges faced during the project include:

- Class imbalance between plant disease categories.
- Similar visual symptoms between some diseases.
- Large dataset size.
- Google Colab free runtime limitations.
- Risk of data leakage caused by duplicate images.
- Need for clear visualization of model performance.

---

## Future Work

Future improvements may include:

- Deploying the model as a web application.
- Deploying the model as a mobile application.
- Testing the model on real-world phone camera images.
- Adding stronger near-duplicate image detection.
- Improving the model using more advanced data augmentation.
- Testing other pretrained models such as ResNet, MobileNet, and EfficientNetV2.
- Adding an automatic disease recommendation system for farmers or agricultural users.

---

## Conclusion

This project demonstrates a Business Intelligence system for plant disease analysis and prediction. It combines deep learning with Power BI visualization to provide both prediction capability and analytical reporting.

The model was built using transfer learning with EfficientNetB0 and evaluated using multiple performance metrics. The results were visualized through an interactive Power BI dashboard, making it easier to analyze model performance, identify class-level strengths and weaknesses, and understand classification behavior across plant disease categories.

The project also included important data quality checks, such as corrupted image detection and duplicate image removal, to reduce the risk of data leakage and improve the reliability of the evaluation.
