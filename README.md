# 🛡️ SpamShield AI — Email Spam Classifier

A machine learning web application that classifies emails as **Spam** or **Not Spam** using a Logistic Regression model, Flask backend, and MongoDB for prediction history.

## 📸 Features

- Paste any email and get an instant spam prediction
- Shows spam probability percentage
- Saves every prediction to MongoDB with timestamp
- History page to view all past predictions
- Clean dark UI built with Bootstrap 5


## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| ML Model | Scikit-learn (Logistic Regression) |
| Vectorizer | TF-IDF (bigrams, 10k features) |
| Database | MongoDB (via PyMongo) |
| Frontend | HTML, CSS, Bootstrap 5 |

---

## 📊 Model Performance

Trained on 5,728 emails (76% ham, 24% spam):

| Class | Precision | Recall | F1 Score |
|---|---|---|---|
| Ham | 98% | 100% | 99% |
| Spam | 99% | 95% | 97% |
| **Overall Accuracy** | | | **98.9%** |

---

## 🚀 Getting Started

### 1. Install Dependencies

```bash
pip install flask scikit-learn pymongo pandas
```

### 2. Make Sure MongoDB is Running

```bash
# MongoDB must be running on localhost:27017
# Default database: spam_classifier_db
# Default collection: history
```

### 3. Train the Model

Run this **once** before starting the app:

```bash
python retrain.py
```

This reads `emails.csv` and generates two files inside the `models/` folder:
- `spam_classifier_model.pkl`
- `feature_extractor.pkl`

### 4. Start the App

```bash
python app.py
```

Then open your browser and go to:
```
http://127.0.0.1:5000
```

---

## 🧪 Testing

You can test via the browser or using the JSON API endpoint:

```bash
curl -X POST http://127.0.0.1:5000/api/predict \
  -H "Content-Type: application/json" \
  -d "{\"message\": \"Congratulations! You won a free iPhone. Click now!\"}"
```

Expected response:
```json
{
  "message": "Congratulations! You won a free iPhone. Click now!",
  "prediction": "Spam",
  "spam_prob": 66.4,
  "raw": 1
}
```

### Sample Test Emails

| Email | Expected Result |
|---|---|
| "Congratulations! You won a free iPhone. Click now!" | 🚫 Spam |
| "Win money fast! Click this link now!" | 🚫 Spam |
| "Hi, please find the report attached." | ✅ Not Spam |
| "Hey, are we still meeting today?" | ✅ Not Spam |

---

## 🔁 Retraining the Model

If you want to retrain with new data, just replace `emails.csv` and run:

```bash
python retrain.py
```

Then restart the app:

```bash
python app.py
```

> **Important:** Always retrain and restart together. Never replace only one `.pkl` file — both must be generated at the same time to stay in sync.

---

## 📝 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Main classifier page |
| POST | `/predict` | Submit email for prediction (form) |
| GET | `/history` | View prediction history |
| POST | `/api/predict` | JSON API for prediction |

---

## ⚠️ Known Issues & Notes

- The model works best on English-language emails
- Very short messages (1-2 words) may have lower confidence
- MongoDB must be running before starting the app or it will error on startup



## 👤 Author
Adeel Hasan Yousfi

Built as a machine learning portfolio project using Flask, Scikit-learn, and MongoDB.

