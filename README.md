# Face Mask Detection with MTCNN

## 📋 Project Overview

This project implements an automated face mask detection system using MTCNN (Multi-task Cascaded Convolutional Networks) for face detection and a deep learning model for mask classification. The system can process multiple images, detect faces, and classify whether each person is wearing a face mask or not.

## 🎯 Key Features

- **Advanced Face Detection**: Uses MTCNN for robust face detection with high accuracy
- **Intelligent Mask Classification**: Pre-trained deep learning model for mask/no-mask classification
- **Automatic Model Interpretation**: Self-correcting system that determines the correct interpretation of model outputs
- **Multiple Preprocessing Techniques**: Enhanced image processing for better face detection in various lighting conditions
- **Fallback Classification**: Color-based mask detection when the primary model fails
- **Batch Processing**: Processes multiple images and displays results in an organized grid
- **Visual Feedback**: Color-coded bounding boxes (Green = Mask, Red = No Mask) with confidence scores

## 🛠️ Technical Architecture

### Core Components

1. **Face Detection Module (MTCNN)**
   - Detects faces with minimum 90% confidence threshold
   - Returns bounding box coordinates and confidence scores
   - Handles multiple faces per image

2. **Mask Classification Pipeline**
   - Preprocesses face regions to model input size
   - Normalizes pixel values (0-1 range)
   - Handles both binary and single-output model architectures

3. **Model Interpretation System**
   - Automatically tests model outputs against known samples
   - Determines correct interpretation mapping
   - Fixes common model output ambiguities

4. **Image Enhancement Pipeline**
   - Brightness adjustment
   - CLAHE (Contrast Limited Adaptive Histogram Equalization)
   - Multiple preprocessing versions for optimal detection

## 🔧 How It Works

### Step-by-Step Process

```
1. Initialization
   ├── Load pre-trained mask classification model
   ├── Initialize MTCNN detector
   └── Set up image paths and parameters

2. Model Calibration
   ├── Test with known mask/no-mask images
   ├── Determine output interpretation
   └── Configure classification function

3. Image Processing Loop
   ├── Load image
   ├── Apply preprocessing techniques
   ├── Detect faces using MTCNN
   ├── For each detected face:
   │   ├── Extract face region
   │   ├── Classify mask presence
   │   ├── Calculate confidence score
   │   └── Draw annotated bounding box
   └── Display results

4. Fallback Mechanisms
   ├── Color-based detection for model failures
   └── HSV color space analysis for mask detection
```

### Key Functions

| Function | Purpose |
|----------|---------|
| `detect_faces_mtcnn()` | Detects faces using MTCNN with configurable confidence threshold |
| `classify_mask()` | Main classification function that determines mask presence |
| `fix_model_interpretation()` | Automatically calibrates model output interpretation |
| `preprocess_face_for_model()` | Prepares face images for model input |
| `classify_mask_simple()` | Fallback color-based mask detection |
| `detect_and_classify_masks()` | Main pipeline orchestrating the entire process |

## 📊 Model Interpretation Logic

The system includes intelligent model interpretation to handle different output formats:

```python
# Handles various model output scenarios:
- Binary classification: [mask_prob, no_mask_prob]
- Inverted binary: [no_mask_prob, mask_prob]  
- Single output: probability value (high = mask or high = no_mask)
```

The calibration process tests known images to determine the correct interpretation automatically.

## 🖼️ Output Visualization

The system provides comprehensive visual feedback:

- **Bounding Boxes**: 
  - Green = Mask detected ✅
  - Red = No mask detected ❌
- **Confidence Scores**: Displayed as percentages (e.g., "Mask (0.95)")
- **Grid Layout**: Multiple images displayed in a 2x3 grid
- **Status Information**: Number of faces detected per image

## 🚀 Usage Example

```python
# Basic usage
if __name__ == "__main__":
    # Step 1: Test model interpretation
    test_model_interpretation()
    
    # Step 2: Calibrate model
    correct_interpretation = fix_model_interpretation()
    
    # Step 3: Run detection on all images
    detect_and_classify_masks()
    
    # Step 4: Analyze specific images
    analyze_single_image('path/to/image.jpg')
```

## 🔍 Error Handling

The system includes robust error handling:
- Graceful fallback when model loading fails
- Alternative classification methods for edge cases
- Duplicate face detection removal
- Empty face region checks
- Exception handling in all critical functions

## 📈 Performance Considerations

- **Confidence Threshold**: Set to 90% for reliable face detection
- **Duplicate Removal**: 30-pixel threshold for identifying duplicate detections
- **Image Preprocessing**: Multiple versions tested for optimal detection
- **Model Input Size**: Automatically detected from loaded model

## 🎨 Customization Options

Key parameters that can be adjusted:
- `min_confidence`: Face detection confidence threshold (default: 0.90)
- `img_size`: Model input size (auto-detected)
- Color ranges for mask detection in HSV space
- Image enhancement parameters (brightness, contrast)

## 📝 Dependencies

- `mtcnn`: Face detection
- `opencv-python (cv2)`: Image processing
- `tensorflow/keras`: Deep learning model
- `numpy`: Numerical operations
- `matplotlib`: Visualization

## 🤝 Contributing

This project demonstrates integration of multiple computer vision techniques for practical mask detection applications. The modular design allows for easy extension and improvement of individual components.
