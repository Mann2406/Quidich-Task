# Quidich Task - Cleaning and Classification
## Summary of Process

1. **Set Up and Run the DFine Detection Model**
   - Cloned the DFine repository (`custom_d_fine.git`) and installed required dependencies (`hydra-core`, `loguru`, `omegaconf`, `tqdm`, `pyyaml`, `pydantic`).
   - Loaded the pre-trained DFine model with weights and processed inputs/outputs to images that conatain football in the `contaminated_dataset/contaminated_classifier_data/football` and `contaminated_dataset/contaminated_classifier_data/background` folders.
   - Updated the 'config.yaml' of the cloned repo to the weights and parameters used for 'config.yaml' of 'model.pt' from the given drive link.
   - Minor changes were made to the 'infer.py' file also since the images were categorized in two folders initally and the initial 'infer.py' had a loop to traverse through only one folder containing images
   - Inference was run using the script `infer_football_background_cleaning_01` to classify images.

2. **Clean the Dataset Using Detection**
   - Implemented a cleaning process in `quidich_task_cleaning.ipynb` to separate images into `cleaned_football` and `cleaned_background` folders based on DFine detections.
   - Moved misclassified images: 1373 misclassified football images were moved from `background` to `football` folder and 3178 background images were correctly classified and organized.
   
3. **Train a Simple Classifier (Optional Bonus)**
   - Trained a ResNet18 classifier(since, faster and near accurate results to ResNet34) on the cleaned dataset using `quidich_task_classifier.ipynb`.
   - Used an 80-20 train-validation split, AdamW optimizer with a learning rate of 0.0001, and 10 epochs.
   - Reported metrics: Training loss decreased from 0.2646 to 0.0420, validation loss stabilized around 0.18-0.23, training accuracy improved from 88.99% to 98.28%, and validation accuracy peaked at 94.51%.

## Number of Images Removed
- Total images processed: ~8279 (5103 football + 3176 background).
- 320 images less were used in the football folder(5103 images instead of 5423) since there was mismatch. But, it generally should perform better with this to prevent class imbalance.

## Assumptions Made
- DFine model accurately detects football content.
- The dataset split (80-20) and hyperparameters are sufficient for initial training.
- No significant overfitting or underfitting occurred based on loss/accuracy trends(it was leaning towards overfitting but no clear signs of it still).

## Classifier Performance and Approach
- The model shows a decreasing training loss and increasing accuracy, indicating good learning. Validation loss and accuracy suggest a stable but not overfitted solution.
- Inference: The model is not overfitting, but a more optimized approach would include early stopping and a learning rate scheduler to prevent overfitting.

## Deliverables
- **Python Scripts**: 
  - `quidich_task_cleaning.ipynb` (dataset cleaning)
  - `quidich_task_classifier.ipynb` (classifier training)
  - both provided here.
    
- **Folder Structure**: 
  - `cleaned_dataset/cleaned_football/` (5103 images)
  - `cleaned_dataset/cleaned_background/` (3176 images)
  - drive link(cleaned dataset & updated custom_d_fine) - https://drive.google.com/drive/folders/1-Cw10tGZ7KQAZ9oQ8LSxNWjDS1kKySeN?usp=sharing

## Additional Notes
- The training plot (included below) visualizes loss and accuracy trends over 10 epochs.

![image](https://github.com/user-attachments/assets/99143f46-7eba-4f8c-894e-2a7d3ba6170d)
