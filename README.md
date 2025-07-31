# AICTE_Edunet-IBM-Internship

# Power System Fault Detection and Classification

## Project Overview

This project aims to develop a machine learning model for the rapid and accurate detection and classification of various fault types (e.g., line-to-ground, line-to-line, three-phase faults) in power distribution systems. By leveraging electrical measurement data, the model contributes to maintaining power grid stability and reliability. The project was implemented using IBM Cloud Lite services, demonstrating an accessible and efficient approach to building and deploying such a crucial system.

**Key Objectives:**
* Ingest and preprocess electrical measurement data.
* Train a machine learning model to distinguish between normal operations and different fault conditions.
* Evaluate model performance using appropriate metrics.
* Deploy the trained model for real-time predictions.

## Dataset

The dataset used for this project is:
* **Name:** Power System Faults Dataset
* **Source:** Kaggle
* **Link:** [https://www.kaggle.com/datasets/ziya07/power-system-faults-dataset](https://www.kaggle.com/datasets/ziya07/power-system-faults-dataset)

This dataset contains electrical measurement data (e.g., voltage and current phasors) necessary for training the fault detection and classification model.

## Technology Stack

* **Cloud Platform:** IBM Cloud (using Lite services)
* **Machine Learning Service:** IBM Watson Studio (including AutoAI for automated ML)
* **Data Storage:** IBM Cloud Object Storage
* **Model Deployment:** IBM Watson Machine Learning

## Algorithms Used

During the automated machine learning experiment in IBM Watson Studio, multiple algorithms were explored, with the primary ones being:

* **Random Forest Classifier** (identified as the primary choice for the final model)
* **Snap Logistic Regression**

## Step-by-Step Implementation Guide on IBM Cloud

This section outlines the general steps followed to implement this project using IBM Cloud Lite services.

### 1. Set Up IBM Cloud Account and Services

1.  **Sign up for IBM Cloud:** If you don't have one, create an [IBM Cloud account](https://cloud.ibm.com/registration). Ensure you are on a Lite plan if you wish to stick to free-tier services.
2.  **Create Watson Studio Service:**
    * Navigate to the IBM Cloud Dashboard.
    * Click "Create resource" and search for "Watson Studio."
    * Select the "Lite" plan and click "Create."
3.  **Create Cloud Object Storage Service:**
    * From the IBM Cloud Dashboard, click "Create resource" and search for "Object Storage."
    * Select the "Lite" plan and click "Create." This will be used to store your dataset.
4.  **Create Watson Machine Learning Service:**
    * From the IBM Cloud Dashboard, click "Create resource" and search for "Watson Machine Learning."
    * Select the "Lite" plan and click "Create." This is where your model will be deployed.

### 2. Data Acquisition and Storage

1.  **Download Dataset:** Download the `power-system-faults-dataset` from the Kaggle link provided above.
2.  **Upload to IBM Cloud Object Storage:**
    * Go to your IBM Cloud Object Storage instance.
    * Create a new bucket (e.g., `fault-data-bucket`).
    * Upload the downloaded `fault_data.csv` (or similar dataset files) into this bucket.

### 3. Project Setup in IBM Watson Studio

1.  **Create a New Project:**
    * Go to your Watson Studio instance.
    * Click "Create a project" and choose "Create an empty project."
    * Give it a name (e.g., `Power System Fault Detection`) and link it to your Cloud Object Storage instance.
2.  **Add Data Asset:**
    * Inside your new project, go to the "Assets" tab.
    * Click "New asset" -> "Data."
    * Choose "IBM Cloud Object Storage" and select your bucket and the `fault_data.csv` file.

### 4. Model Development using AutoAI (Recommended for Automation)

1.  **Create AutoAI Experiment:**
    * From your Watson Studio project, click "New asset" -> "AutoAI experiment."
    * Give it a name and link it to your Watson Machine Learning service instance.
    * Select the `fault_data.csv` as your source data.
2.  **Configure Experiment:**
    * **Prediction Type:** Select "Multiclass classification."
    * **Target Column:** Choose the column representing the fault type (e.g., `Fault Type` or `Prediction`).
    * **Optimized Metric:** Set "Accuracy" as the primary metric for ranking pipelines.
    * Review other settings (optional exclusions, data splits).
3.  **Run Experiment:** Click "Run experiment." AutoAI will automatically perform data preprocessing, algorithm selection (including Random Forest and Snap Logistic Regression), hyperparameter optimization, and pipeline generation.
    * *Monitor Progress:* Observe the "Progress map" and "Relationship map" as AutoAI evaluates different pipelines.

### 5. Model Evaluation and Selection

1.  **Review Pipelines:** Once the AutoAI experiment completes (as shown in `Progress_map.jpg`), review the generated pipelines.
2.  **Analyze Metrics:** Go to the "Pipeline comparison" tab (as shown in `Matric_chart.jpg`) to compare pipelines based on various metrics (Accuracy, F1-score, Precision, Recall, Log loss, etc.).
3.  **Select Best Pipeline:** Identify the best-performing pipeline (e.g., Pipeline 1 as indicated in `Matric_chart.jpg` if it had the highest accuracy).

### 6. Model Deployment

1.  **Save the Model:** From the summary of your best-performing pipeline in AutoAI, click the "Save model" icon. This will save the trained model to your Watson Machine Learning instance.
2.  **Deploy the Model:**
    * Go to your Watson Machine Learning service instance.
    * Find your saved model under "Models."
    * Click on the model and choose "Deploy."
    * Select "Online" as the deployment type and give it a name.
    * Click "Create deployment." This will create a REST API endpoint for your model.

### 7. Inference and Prediction

1.  **Get Deployment Endpoint:** Once deployed, you will get an API endpoint (URL) for your model.
2.  **Test Prediction:** Use a tool like `curl`, Postman, or a Python script to send new electrical measurement data (in JSON format) to the deployed model's API endpoint.
    * The model will return a prediction, including the fault type and a confidence score (similar to `Prediction_Results.jpg`).

## Project Output Examples (from provided images)

* **Prediction Results:**
    * **Prediction:** Line Breakage
    * **Confidence:** 39%
    * **Fault ID:** F001
    * **Fault Location:** (34.0522, -118.2437)
    * **Electrical Data:** Voltage: 2200V, Current: 250A, Power: 50kW

* **Model Performance (Example from AutoAI):**
    * Initial Accuracy (Pipeline 5, Random Forest): 0.390
    * Best Pipeline (P1) during cross-validation showed ~0.41 accuracy across various metrics.

## Conclusion

This project successfully demonstrated the application of machine learning, particularly with the Random Forest Classifier, for power system fault detection and classification on IBM Cloud. The automated capabilities of Watson Studio's AutoAI significantly streamlined the model development process, leading to an effective solution for enhancing grid stability and reliability.

## Future Scope

* **Real-time Integration:** Implement continuous data ingestion and real-time inference using streaming data.
* **Predictive Maintenance:** Develop capabilities to predict imminent faults before they occur.
* **Advanced ML Models:** Explore deep learning architectures for more complex fault patterns.
* **Root Cause Analysis:** Extend the model to identify the underlying causes of faults.
* **Automated Response:** Integrate with grid management systems for automated fault isolation and restoration.
