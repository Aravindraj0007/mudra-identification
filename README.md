# 🙏 Mudra Identification System

A real-time hand gesture (mudra) detection system with a modern web interface, using OpenCV, MediaPipe, and Flask to recognize classical Indian dance mudras from webcam input.

## ✨ Features

- **🌐 Web-Based Interface**: Modern, responsive web application accessible via browser
- **📹 Real-time Detection**: Live webcam feed with instant mudra recognition
- **🤚 25+ Mudras Supported**: Recognizes over 25 classical mudras including:
  - Pataka, Tripataka, Ardhachandra
  - Kartarimukha, Mukula, Hamsasya
  - Bhramara, Chatura, Arala, Suchi
  - Musti, Sikharam, Mayura, Kapittha
  - And many more traditional hand gestures...
- **🎯 Visual Feedback**: Real-time mudra detection with color-coded status indicators
- **📊 Hand Landmark Visualization**: MediaPipe hand landmarks overlaid on video feed
- **🎛️ Camera Controls**: Toggle camera on/off functionality
- **📚 Mudra Information**: Detailed descriptions and cultural context for each mudra
- **🔌 REST API**: RESTful endpoints for integration with other applications
- **📱 Responsive Design**: Works on desktop, tablet, and mobile devices

## 📋 Requirements

- **Python**: 3.7 or higher
- **Dependencies**:
  ```
  opencv-python==4.8.1.78
  mediapipe==0.10.20
  flask==3.0.0
  ```

## 🚀 Quick Start

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Aravindraj0007/mudra-identification.git
   cd mudra-identification
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   Or install individually:
   ```bash
   pip install opencv-python mediapipe flask
   ```

### Running the Application

#### Web Application (Recommended)
```bash
python app.py
```
Then open your browser and navigate to: `http://localhost:5000`

#### Command Line Version
```bash
python main.py
```

### 🎮 Usage Instructions

#### Web Interface
1. **Start the Application**: Run `python app.py`
2. **Open Browser**: Navigate to `http://localhost:5000`
3. **Camera Access**: Allow camera permissions when prompted
4. **Perform Mudras**: Position your hand in front of the camera
5. **View Results**: See real-time detection results and mudra information
6. **Camera Controls**: Use the toggle button to turn camera on/off

#### Desktop Version
- The webcam window opens automatically
- Perform mudras in front of the camera
- Press **'q'** to quit the application

## 📁 Project Structure

```
mudra-identification/
├── app.py                  # Flask web application (main entry point)
├── main.py                 # Core mudra detection algorithms
├── mudra_info.py          # Mudra information and descriptions database
├── requirements.txt        # Python dependencies
├── start_web.sh           # Shell script to start web server
├── mudra images.pdf       # Reference images for mudras
├── README.md              # Project documentation
├── images/                # Mudra reference images
│   ├── Pataka.jpg
│   ├── Tripataka.jpg
│   ├── Ardhachandra.jpg
│   └── ... (25+ mudra images)
├── static/                # Web application assets
│   ├── style.css         # CSS styles
│   └── script.js         # JavaScript functionality
└── templates/             # HTML templates
    └── index.html        # Main web interface
```

## 🔧 How It Works

### Architecture Overview
The system consists of three main components:

1. **🎥 Computer Vision Pipeline**:
   - **Hand Landmark Detection**: Uses MediaPipe Hands to detect 21 hand landmarks in real-time
   - **Distance Normalization**: Calculates scale-invariant distances between landmarks
   - **Finger Analysis**: Determines finger positions (straight/bent) using geometric ratios
   
2. **🧠 Mudra Recognition Engine**:
   - **Feature Extraction**: Analyzes finger positions, distances, and angles
   - **Pattern Matching**: Applies specific algorithms for each mudra type
   - **Priority-based Classification**: Uses hierarchical matching to avoid false positives
   
3. **🌐 Web Interface**:
   - **Flask Backend**: Serves API endpoints and handles video streaming
   - **Real-time Processing**: Processes video frames and returns mudra results
   - **RESTful API**: Provides endpoints for mudra information and camera controls

### Detection Process
1. **Frame Capture**: Captures video from webcam
2. **Hand Detection**: MediaPipe identifies hand presence and landmarks
3. **Feature Computation**: Calculates distances, angles, and finger states
4. **Mudra Classification**: Matches features against known mudra patterns
5. **Result Display**: Shows detected mudra with confidence indicators

### Technical Details

#### Key Functions
- `is_finger_straight()`: Checks if a finger is straight using MCP→PIP→TIP distance ratios
- `compute_distance_tables()`: Pre-computes all pairwise distances between landmarks
- `get_scale_ref()`: Calculates palm width for scale-invariant detection
- Individual mudra detection functions (e.g., `is_pataka_mudra()`, `is_mukula_mudra()`)

#### Detection Algorithm
The system uses a combination of:
- **Geometric constraints**: Distance ratios between fingertips
- **Angle measurements**: Relative orientation of fingers
- **Bounding box analysis**: Clustering of fingertips (for mudras like Mukula)
- **Threshold-based classification**: Adjustable thresholds for different hand sizes

## 🔗 API Endpoints

The Flask application provides several REST API endpoints:

| Endpoint | Method | Description |
|----------|---------|-------------|
| `/` | GET | Main web interface |
| `/video_feed` | GET | Live video stream with mudra detection |
| `/current_mudra` | GET | Current detected mudra status |
| `/mudra_list` | GET | List of all supported mudras |
| `/mudra_info/<name>` | GET | Detailed information about specific mudra |
| `/toggle_camera` | POST | Toggle camera on/off |
| `/camera_status` | GET | Current camera status |
| `/images/<filename>` | GET | Serve mudra reference images |

### Example API Usage
```javascript
// Get current mudra
fetch('/current_mudra')
  .then(response => response.json())
  .then(data => console.log('Current mudra:', data.mudra));

// Toggle camera
fetch('/toggle_camera', { method: 'POST' })
  .then(response => response.json())
  .then(data => console.log('Camera status:', data.status));
```

## 🤚 Supported Mudras

| Mudra Name | Description | Cultural Significance |
|------------|-------------|----------------------|
| **Pataka** | All fingers straight, thumb tucked | Flag gesture, represents honor and respect |
| **Tripataka** | Index, middle, pinky straight; ring bent | Three parts of fire, represents trinity |
| **Ardhachandra** | Fingers in crescent moon shape | Half moon, represents beauty and grace |
| **Kartarimukha** | Index & middle extended, ring & pinky bent | Scissors face, cutting or separation |
| **Mayura** | Peacock-like finger arrangement | Represents the beautiful peacock |
| **Arala** | Index bent touching thumb, others straight | Bent gesture, represents obstacles overcome |
| **Suchi** | Index finger pointed, others closed | Needle, represents precision and focus |
| **Musti** | Closed fist formation | Represents strength and determination |
| **Sikharam** | Peak-like finger arrangement | Mountain peak, represents achievement |
| **Kapittha** | Wood apple mudra formation | Represents the kapittha fruit |
| **Katakamukha** | Opening/bracket-like formation | Represents an opening or entrance |
| **Sarpashirsa** | Snake head formation | Represents wisdom and transformation |
| **Mrugashirsha** | Deer head formation | Represents gentleness and alertness |
| **Simhamukha** | Lion face formation | Represents courage and power |
| **Kangula** | Bracelet-like formation | Represents adornment and beauty |
| **... and more** | 25+ classical mudras supported | Each with unique cultural meaning |

## 🛠️ Troubleshooting

### 🚫 Mudra Not Detecting
- **💡 Lighting**: Ensure bright, even lighting without shadows
- **📍 Hand Position**: Keep hand clearly visible and centered in frame
- **📏 Distance**: Maintain 30-60 cm from camera for optimal detection
- **🎨 Background**: Use plain, contrasting background (avoid busy patterns)
- **✋ Mudra Form**: Ensure accurate mudra formation per classical definitions
- **📹 Camera Quality**: Higher resolution cameras provide better detection

### 🐌 Performance Issues
- **💻 System Resources**: Close unnecessary applications
- **📹 Camera Settings**: Check if other apps are using the webcam
- **🌐 Browser**: Use Chrome/Firefox for best web interface performance
- **🔧 Settings**: Reduce video quality if needed in browser settings

### 🌐 Web Interface Issues
- **🔌 Port Conflicts**: Ensure port 5000 is available
- **🛡️ Firewall**: Check if firewall is blocking the application
- **📱 Mobile Access**: Use responsive design features on mobile devices
- **🔄 Refresh**: Reload the page if video feed stops working

## ⚙️ Configuration

### Detection Sensitivity
Adjust detection thresholds in `main.py`:

```python
# Example: Modify finger straightness sensitivity
is_finger_straight(landmarks, dist_table, ndist_table, 5, 6, 8, threshold=0.85)
```
- **Lower threshold (0.7-0.8)**: More relaxed detection (detects partial mudras)
- **Higher threshold (0.9-0.95)**: Stricter detection (requires precise formation)

### Camera Settings
Modify camera parameters in `app.py`:

```python
# Adjust camera resolution and FPS
camera.set(cv2.CAP_PROP_FRAME_WIDTH, 1280)    # Width
camera.set(cv2.CAP_PROP_FRAME_HEIGHT, 720)    # Height  
camera.set(cv2.CAP_PROP_FPS, 30)              # Frame rate
```

### Web Server Configuration
```python
# Change host and port in app.py
app.run(
    host='0.0.0.0',    # '127.0.0.1' for local only
    port=5000,         # Change port if needed
    debug=True         # Enable for development
)
```

## 🤝 Contributing

We welcome contributions! Here are ways you can help:

### 🆕 Adding New Features
- **New Mudras**: Implement detection algorithms for additional mudras
- **UI Improvements**: Enhance the web interface design and usability  
- **Mobile Support**: Improve responsive design for mobile devices
- **Performance**: Optimize detection algorithms and video processing

### 🐛 Bug Reports
- **Issues**: Report bugs via GitHub issues with detailed descriptions
- **Testing**: Help test the application on different systems and cameras
- **Documentation**: Improve or translate documentation

### 💻 Development Setup
```bash
# Fork and clone the repository
git clone https://github.com/your-username/mudra-identification.git
cd mudra-identification

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install development dependencies
pip install -r requirements.txt
pip install pytest flask-testing  # Additional dev tools

# Run tests
python -m pytest tests/

# Start development server
python app.py
```

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**Open Source**: Free for educational, research, and commercial use with attribution.

## 🙏 Acknowledgments

- **[MediaPipe](https://mediapipe.dev/)**: Google's powerful hand tracking and pose estimation
- **[OpenCV](https://opencv.org/)**: Comprehensive computer vision library
- **[Flask](https://flask.palletsprojects.com/)**: Lightweight and flexible web framework
- **Classical Dance Community**: For preserving and documenting traditional mudra knowledge
- **Contributors**: All developers who have contributed to this project

## 🚀 Future Roadmap

### 🎯 Planned Features
- [ ] **Two-Hand Mudras**: Support for complex two-handed gestures
- [ ] **Sequence Recognition**: Detect mudra transitions and dance sequences  
- [ ] **Learning Mode**: Interactive tutorials with real-time feedback
- [ ] **Mobile App**: Native iOS/Android applications
- [ ] **AR Integration**: Augmented reality mudra guidance
- [ ] **Multi-language**: Interface in multiple languages
- [ ] **Data Export**: Export detection sessions for analysis
- [ ] **Custom Training**: Allow users to train custom mudras
- [ ] **Cloud API**: RESTful cloud service for mudra detection
- [ ] **Gesture Recording**: Record and playback mudra sequences

### 🌍 Community Goals
- [ ] **Cultural Documentation**: Partner with dance institutions
- [ ] **Accessibility**: Support for differently-abled users
- [ ] **Educational Integration**: Curriculum for schools and universities
- [ ] **Research Platform**: Tools for academic mudra studies

---


---

**⚡ Quick Start**: `pip install -r requirements.txt && python app.py` → Open `http://localhost:5000`

**🎭 Cultural Note**: This system is designed to preserve and promote the beautiful art of classical Indian mudras. Each gesture carries deep cultural significance and represents centuries of artistic tradition. We encourage users to learn about the cultural context and meaning behind these sacred hand positions.

