# Task III – Knee CT Scan Feature Extraction and Comparison
This repository contains the implementation of the feature extraction and comparison pipeline for 3D knee CT scans, as assigned in Task III of the medical imaging challenge.
Objective
To build a complete pipeline that:
1.	Segments a 3D knee CT scan into three anatomical regions: Tibia, Femur, and Background.
2.	Converts a 2D pretrained DenseNet121 model into a 3D CNN.
3.	Extracts deep feature representations from each region.
4.	Compares these features using cosine similarity.
5.	Organizes and saves the results in a CSV file.
________________________________________
Dataset
•	A 3D CT scan file was provided in Task 1.
•	It includes both image volume and corresponding segmentation masks indicating:
o	Tibia (green mask)
o	Femur (red mask)
o	Background (remaining region)
________________________________________
Pipeline Overview
1. Segmentation-Based Splitting
•	Extracts the tibia, femur, and background volumes from the 3D mask.
2. Model Conversion – 2D to 3D DenseNet121
•	Loads a pretrained 2D DenseNet121 model from torchvision.
•	Inflates all Conv2D layers into Conv3D:
o	Expands filters along depth.
o	Normalizes weights by depth to retain activation scale.
3. Feature Extraction
•	For each region (Tibia, Femur, Background):
o	Passes 3D volume through the 3D CNN.
o	Extracts feature maps from:
	Last convolutional layer
	Third-last convolutional layer
	Fifth-last convolutional layer
o	Applies Global Average Pooling (GAP) to convert feature maps to 1D vectors.
4. Feature Comparison
•	Computes cosine similarity between feature vectors from:
o	Tibia ↔ Femur
o	Tibia ↔ Background
o	Femur ↔ Background
•	Done for each of the three selected layers.
5. Result Organization
•	Stores the cosine similarity scores in a CSV file.
•	Each row represents one scan/image and one convolutional depth level.
