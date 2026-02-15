# System Design Document

## 1. Architecture Overview

The Wildlife Conflict Mitigation System follows a modular architecture consisting of:

1. Multi-Sensor Data Acquisition Module
2. AI Processing Module (Image and Audio)
3. ML-Based Validation Module
4. Context Processing Module
5. Animal Knowledge and LLM Response Module
6. Alert Generation and Communication Module
7. Historical Incident Database
8. Risk Prediction Module

---

## 2. System Workflow

1. Image or audio input is received from a sensor along with metadata (zone, timestamp).
2. YOLOv8 performs wildlife detection on image input.
3. Audio CNN classifies animal sounds from audio input.
4. The ML validation model filters detections based on confidence and contextual features.
5. The context processor enriches detection data using zone mapping, time of day, and historical risk.
6. The LLM module generates species-specific safety instructions.
7. The alert engine structures and sends notifications to villagers.
8. A temporary chat group is created for coordinated response.
9. Detection and incident data are logged in the historical database.
10. The risk prediction model updates zone-level risk scores based on accumulated data.

---

## 3. AI Components

### Image Detection
YOLOv8 (PyTorch) is used for detecting wildlife species from camera images.

### Audio Detection
A CNN model (TensorFlow/Keras) processes Mel-spectrograms generated from audio signals to classify animal sounds.

### Validation Model
Logistic Regression or Random Forest (Scikit-learn) is used to filter false positives and validate detections.

### Risk Prediction
A Random Forest model analyzes historical incident data to forecast high-risk zones and time periods.

---

## 4. Communication Design

- Alerts are generated with species, zone, risk level, confidence score, and safety instructions.
- Notifications are delivered via SMS or push notification services.
- A temporary real-time chat room is created for incident coordination.
- All alert activities are logged for monitoring and learning.

---

## 5. Data Storage Design

The historical database stores:

- Species detected
- Confidence score
- Zone information
- Timestamp
- Risk classification
- Alert delivery status
- Incident reports
- Damage outcomes

This data supports validation improvement and predictive risk modeling.

---

## 6. Scalability Considerations

- Modular architecture allows independent scaling of AI inference and communication services.
- Database-driven design enables deployment across multiple villages.
- Risk prediction models improve over time through continuous data logging.
