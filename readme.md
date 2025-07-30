# Egyptian License Plate Recognition 🇪🇬

An advanced end-to-end OCR system for detecting Egyptian vehicle license plates and recognizing their Arabic characters using custom YOLOv8 models.

---

## 🔥 Key Features

- 🚗 **License Plate Detection**: Detects plates in car images using a YOLOv8 model.
- 🔠 **Character Detection**: Identifies individual Arabic letters and numbers on the plate.
- 🔁 **Bidirectional Text Assembly**: Reconstructs Arabic plate numbers with RTL letters and LTR digits.
- 🖼️ **Visual Output**: Annotates original images with plate boxes and rendered Arabic text.
- 🧾 **Final Output**: Saves the plate text and an annotated image file for review.

---

## 📁 Project Structure

```
project/
├── detect_plate_and_chars.py         # Main OCR pipeline script
├── best.pt                           # Trained YOLOv8 license plate detection model
├── chars.pt                          # Trained YOLOv8 Arabic character detection model
├── dataset/                          # Training datasets
│   ├── EALPR- Plates dataset/        # Vehicle plate images
│   └── EALPR- LP characters dataset/ # Character-level images and labels
└── README.md                         # This documentation file
```

---

## 🏋️ Model Training

### 1️⃣ License Plate Detector

Use the following YOLOv8-compatible YAML structure:

```yaml
train: ../content/datasets/jox/Vehicles/train
val: ../content/datasets/jox/Vehicles Labeling/val
nc: 1
names: ['License Plate']
```

Train with:

```bash
yolo task=detect mode=train model=yolov8n.pt \
     data=plate_data.yaml epochs=50 imgsz=640
```

### 2️⃣ Character Detector

YAML file format:

```yaml
train: dataset/yolo_ready/train/images
val: dataset/yolo_ready/val/images
nc: 27
names:
  0: أ
  1: ب
  2: ج
  3: د
  4: ر
  5: س
  6: ص
  7: ط
  8: ع
  9: ف
  10: ق
  11: ل
  12: م
  13: ن
  14: ھ
  15: و
  16: ى
  17: ٠
  18: ١
  19: ٢
  20: ٣
  21: ٤
  22: ٥
  23: ٦
  24: ٧
  25: ٨
  26: ٩
```

Train with:

```bash
yolo task=detect mode=train model=yolov8n.pt \
     data=character_data.yaml epochs=100 imgsz=320
```

---

## 🧪 Inference Pipeline

Run the OCR script:

```bash
python detect_plate_and_chars.py
```

This script will:

- Load YOLOv8 models for plate and character detection
- Detect the license plate from the input image
- Crop the plate and detect characters within it
- Sort characters (RTL for letters, LTR for digits)
- Reconstruct the final plate string
- Overlay the text and bounding box on the original image
- Save the annotated result as `annotated_plate.jpg`

### ✅ Sample Output:

- Final Plate Text: `ط د و ٩٢٦٧`
- Annotated Image: `annotated_plate.jpg`

---

## 🔡 Character Mapping

Used in the script for ID-to-character conversion:

```python
id2char = {
  0: 'أ', 1: 'ب', 2: 'ج', 3: 'د', 4: 'ر', 5: 'س', 6: 'ص',
  7: 'ط', 8: 'ع', 9: 'ف', 10: 'ق', 11: 'ل', 12: 'م', 13: 'ن',
  14: 'ھ', 15: 'و', 16: 'ى', 17: '٠', 18: '١', 19: '٢',
  20: '٣', 21: '٤', 22: '٥', 23: '٦', 24: '٧', 25: '٨', 26: '٩'
}
```

---

## 📦 Installation

Install the required packages:

```bash
pip install ultralytics opencv-python torch numpy arabic_reshaper python-bidi pyautogui
```

---

## 📄 License

MIT License — free for personal, academic, or commercial use.

---

## 🙌 Acknowledgments

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
- EALPR: Egyptian Automatic License Plate Recognition dataset

---
## 📥 Dataset

You can download the full training dataset used for this project from the following link:

👉 [Download Egyptian Plate OCR Dataset (Google Drive)](https://drive.google.com/file/d/1l3P7tpLPCcI6N0p8T9uxW3NL0GJXKPnA/view?usp=drive_link)


---
## 🌐 Live Demo

Try a live run of the OCR system here:

🚀 [Launch Live Demo]([https://your-live-demo-link.com](https://drive.google.com/file/d/1ijQsaZnpCnqJoQAa-gEGxrgQA-dqtp8o/view?usp=sharing))
---

## 🤝 Contributing

Want to help? You can:

- Improve detection accuracy
- Expand the dataset
- Optimize Arabic text rendering

Pull requests and issues are welcome!

