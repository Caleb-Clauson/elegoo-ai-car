# **ELEGOO-AI-Smart-car**
This project demonstrates how to control an **Elegoo Smart Car** using **real-time image classification** with a **TensorFlow Lite** model.  
The car is guided based on predictions made from the live video feed captured by an **ESP32-CAM** module mounted on the car. The car's AI is trained on stop sing, stop light, and pedestrians, allowing it to stop and watch out for these items.

The system identifies objects (such as people or stop signs or traffic lights) and commands the car to move forward, stop, or turn based on the classification results.

---

## **⚙️ Requirements**

- Python 3.12
- Packages:
  - `tensorflow`
  - `numpy`
  - `pillow`
  - `everywhereml`
  - `opencv-python`
  - `socket`
  - `time`
  - `os`

---

## **🛠️ Setup Instructions**

### 1. Set Up Virtual Environment (Recommended)

```bash
python3 -m venv venv
source venv/bin/activate        # On macOS/Linux
venv\Scripts\activate           # On Windows
```

### 2. Install Python Packages

```bash
pip install -r requirements.txt
```

### 3. Prepare Model Files
- Place your `keras_model.h5` and `labels.txt` files in the same folder as `main.py`.
- Ensure the labels correspond exactly to the model’s outputs.

### 4. Configure Script Settings
Inside `main.py`, edit these variables to match your setup:

```python
MODEL_PATH = "keras_model.h5"   # Path to your Keras model
LABELS_PATH = "labels.txt"      # Path to your labels
ESP_CAMERA_IP = "192.168.X.X"   # IP address of your ESP32-CAM
```

Make sure your **ESP32-CAM is connected** to the same network as your computer and that its **IP address** is correctly set.

---

## **🚗 How It Works**

1. **Load the Machine Learning Model**  
   The model is loaded from the `.h5` file using TensorFlow Lite Interpreter.

2. **Capture Frames from ESP32-CAM**  
   The script continuously fetches images from the ESP32 camera over HTTP.

3. **Preprocess Frames**  
   Images are resized and normalized to match the model's input requirements.

4. **Run Inference**  
   Each frame is classified. The model outputs a probability distribution over known classes.

5. **Send Commands to the Car**  
   Based on the top prediction and its confidence, appropriate driving commands are sent to the Elegoo Smart Car over a socket connection.

| Prediction        | Car Behavior           |
|-------------------|-------------------------|
| Person Detected    | Stop           |
| Stop Sign Detected | Stop or Slow down            |
| Unknown or Low Confidence | Stay still or slow turn |

6. **Handle Connectivity**  
   Automatic reconnection attempts are made if the car’s socket connection is lost.

---

## **📈 Important Tips for Beginners**

- **Always verify your ESP32-CAM IP address.**  
  (It often changes after power cycles!)

- **Normalize image pixel values between 0 and 1** when preparing the input for TensorFlow models.

- **Handle low confidence outputs carefully.**  
  (Don’t issue drastic commands based on poor predictions.)

- **Use a Virtual Environment** to avoid dependency conflicts.

- **Check that your labels match the model output exactly** to avoid mismatches.

- **Log your predictions and actions** during testing for easier debugging.

---

## **📺 Video Walkthrough**

[Click here to watch the project walkthrough on YouTube!(https://youtu.be/5SP6lWJdkx0)]

In the video, I explain:
- How I installed everything
- How I configure'd my system with Virtual Environments
- Issues my group and I faced durring the project
