![P_curve](https://github.com/user-attachments/assets/b8457700-088c-41bd-90d9-adb6666c4c56)Here’s a `README.md` template for your image classification project using YOLOv8 for classifying apples into "fresh-apple," "rotten-apple," and "mild-apple" categories.

---

# YOLOv8 Apple Classification Project

This project uses the YOLOv8 model to classify apples into three categories: fresh, rotten, and mild. The dataset was annotated using Roboflow and includes labeled images for training the YOLOv8 model on this classification task.

## Dataset

- **Source**: [Roboflow Fruit Classification Dataset](https://app.roboflow.com/fruitclassification-djarn/fruit_classification-uozc4/1/export)
- **Classes**: 
  - `fresh-apple`
  - `rotten-apple`
  - `mild-apple`

## Project Structure

- `data/`: Directory for training and test images.
- `notebooks/`: Contains the Colab notebook used for training and testing.
- `results/`: Directory to store the trained model and prediction outputs.

## Requirements

- Python 3.x
- YOLOv8 (installed via `ultralytics` package)
- Google Colab and Google Drive for storage

## Installation

1. Clone the repository and navigate to the project folder:
    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    cd your-repo-name
    ```

2. In the Google Colab notebook, install the required packages:
    ```python
    !pip install ultralytics
    ```

## Usage

The following steps explain how to use the Colab notebook to train and test the model.

1. **Set Up Google Drive**: Mount Google Drive to access and save files.
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. **Install YOLOv8**:
   ```python
   !pip install ultralytics
   from ultralytics import YOLO
   ```

3. **Train the Model**:
   - Define the path to the YOLOv8 model and data configuration file.
   - Start the training process with specified epochs and image size.
   ```python
   model = YOLO("yolov8m.pt")
   ROOT_DIR = '/content/drive/MyDrive/yolov8-classi04'
   results = model.train(data=os.path.join(ROOT_DIR, "data.yaml"), epochs=20, imgsz=640)
   ```

4. **Save Results to Google Drive**:
   - Copy the results to Google Drive to retain training outputs.
   ```python
   import shutil
   destination = '/content/drive/MyDrive/yolov8-classi04-results'
   if os.path.exists(destination):
       shutil.rmtree(destination)
   shutil.copytree('/content/runs', destination)
   ```

5. **Make Predictions**:
   - Use the trained model to make predictions on new images.
   ```python
   model = YOLO("/content/drive/MyDrive/yolov8-classi04-results/detect/train/weights/best.pt")
   results = model.predict("/content/drive/MyDrive/yolov8-classi04/test1.jpg", save=True, save_txt=True, imgsz=640, conf=0.2)
   ```

## Example Output

Sample predictions will include classifications into the three categories (fresh-apple, rotten-apple, mild-apple) along with bounding boxes and confidence scores.

```
Image: test1.jpg
Predicted Class: fresh-apple
Confidence: 0.87
```

## Results

- **Model Accuracy**:
![F1_curve](https://github.com/user-attachments/assets/849f2b39-3a43-44da-8e4d-566a95e3d345)
![confusion_matrix_normalized](https://github.com/user-attachments/assets/e050b891-8339-4e72-aaae-15c7ac95dba5)
![confusion_matrix](https://github.com/user-attachments/assets/ae57fb4c-fc3a-40cc-a7cb-98cc1d77c260)
![results](https://github.com/user-attachments/assets/a230063d-3a1e-4d87-b988-494a7085ce8d)
![R_curve](https://github.com/user-attachments/assets/652f863b-cf36-4557-b514-54408adeb252)
![PR_curve](https://github.com/user-attachments/assets/4fc423e3-e404-4ea8-850c-823137da2a83)
- **Model Validation Images**:
![val_batch2_pred](https://github.com/user-attachments/assets/eb817342-06e1-4700-a434-96b33ef0e77e)
![val_batch2_labels](https://github.com/user-attachments/assets/53851b45-c803-4ba0-9cc1-949521b202e8)
![val_batch1_pred](https://github.com/user-attachments/assets/a3c54435-91d8-422a-a159-49c9f4672370)
![val_batch1_labels](https://github.com/user-attachments/assets/ef2da100-1237-4039-91ef-1b37d55d9760)
![val_batch0_pred](https://github.com/user-attachments/assets/bc06ed48-b005-42f9-b5be-5d686802565e)
- **Model Prediction Images**:
- ![test3](https://github.com/user-attachments/assets/0483afa4-6458-4bc1-b8af-e5bcf0dfe912)
![test2](https://github.com/user-attachments/assets/4a668bc9-55df-49a7-b6ef-310f2c4bace0)
![test1](https://github.com/user-attachments/assets/395ab477-012e-40bd-a738-28ac97deb025)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
