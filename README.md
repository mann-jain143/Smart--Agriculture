# OPTI-CROP - Smart Crop Recommendation System

OPTI-CROP is an intelligent crop recommendation system powered by machine learning that helps farmers make data-driven decisions about which crops to plant based on soil nutrients, climate conditions, and rainfall patterns.

## Features

- **Machine Learning Model**: Random Forest classifier trained on crop-soil-climate data
- **43+ Crop Support**: Recommendations for diverse crops including cereals, pulses, vegetables, and fruits
- **Real-time Predictions**: Instant crop recommendations with confidence scores
- **Comprehensive Analysis**: 
  - Top 3 crop recommendations with confidence percentages
  - Radar chart comparing user inputs vs ideal conditions
  - Parameter-wise advice for optimization
  - Match quality assessment (Excellent/Good/Best Available)
- **Responsive UI**: Modern, colorful dashboard with Bootstrap 5
- **Session History**: Tracks recent predictions for quick reference

## Tech Stack

- **Backend**: Flask 3.0.0
- **ML Framework**: scikit-learn 1.4.1
- **Data Processing**: pandas 2.2.0, numpy 1.26+
- **Frontend**: Bootstrap 5.3.2, Chart.js
- **Environment**: Python 3.13

## Installation

### Prerequisites
- Python 3.13+
- pip (Python package manager)

### Setup

1. **Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/OPTI-CROP.git
cd OPTI-CROP
```

### Setup & Launch

The project is split into a **backend** Flask API and a **frontend** React + Vite SPA.

#### 1. Backend Setup (Flask API)
1. **Navigate to backend and create virtual environment**
   ```bash
   cd backend
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```
2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the Flask server**
   ```bash
   python app.py
   ```
   The backend API will run on `http://localhost:5000`

#### 2. Frontend Setup (React + Vite)
1. **Navigate to frontend**
   ```bash
   cd ../frontend
   ```
2. **Install node dependencies**
   ```bash
   npm install
   ```
3. **Run the development server**
   ```bash
   npm run dev
   ```
   The application dashboard will be available at `http://localhost:5173`

## API Endpoints

### GET /
Returns the home page with the crop recommendation form.

**Response**: HTML template

---

### POST /predict
Submits soil and climate parameters to get crop recommendations.

**Request Body** (form-data):
```
N: number (0-140) - Nitrogen in kg/ha
P: number (0-145) - Phosphorus in kg/ha
K: number (0-205) - Potassium in kg/ha
temperature: number (0-45) - Temperature in °C
humidity: number (0-100) - Relative humidity in %
ph: number (0-14) - Soil pH
rainfall: number (0-300) - Rainfall in mm
```

**Response**: HTML with:
- Recommended crop
- Top 3 crop options with confidence scores
- Radar chart comparing inputs vs ideal conditions
- Parameter adjustment advice
- Crop growing profile and tips

---

## Testing with Postman

### Example 1: Paddy Recommendation
```
POST http://localhost:5000/predict

Body (form-data):
N: 80
P: 40
K: 40
temperature: 25
humidity: 80
ph: 6.0
rainfall: 175
```

### Example 2: Wheat Recommendation
```
POST http://localhost:5000/predict

Body (form-data):
N: 100
P: 40
K: 40
temperature: 17
humidity: 65
ph: 6.8
rainfall: 70
```

### Example 3: Tomato Recommendation
```
POST http://localhost:5000/predict

Body (form-data):
N: 80
P: 40
K: 40
temperature: 23
humidity: 70
ph: 6.5
rainfall: 100
```

## Supported Crops

**Cereals**: Paddy, Maize, Rice, Wheat, Barley, Millet

**Pulses**: Chickpea, Pea, Lentil

**Oilseeds**: Soybean, Groundnut, Sunflower, Mustard

**Spices**: Coffee, Tea, Chilli, Garlic, Ginger, Turmeric

**Vegetables**: Tomato, Cabbage, Lettuce, Spinach, Onion, Broccoli, Carrot, Cucumber, Pumpkin

**Fruits**: Banana, Orange, Apple, Grapes, Mango, Coconut, Lemon, Pineapple, Papaya, Pomegranate

**Cash Crops**: Sugarcane, Cotton, Watermelon

## Project Structure

```
OPTI-CROP/
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── .env                           # Environment variables (not in git)
├── .gitignore                     # Git ignore rules
├── dataset.csv                    # Training dataset (not in git)
├── models/                        # ML model artifacts (not in git)
│   ├── crop_recommendation_model.pkl
│   └── scaler.pkl
├── static/
│   ├── css/
│   │   └── styles.css            # Custom styling
│   └── img/                       # Crop images
└── templates/
    └── index.html                # Main UI template
```

## How It Works

1. **Input Validation**: Validates that all parameters are numeric and non-negative
2. **Feature Scaling**: Normalizes input values using StandardScaler
3. **Model Prediction**: Random Forest model predicts crop probabilities
4. **Match Scoring**: Compares user inputs against ideal conditions for each crop
5. **Recommendation Logic**:
   - Finds first crop with "Excellent" match (avg difference ≤ 10)
   - Falls back to "Good" match (avg difference ≤ 20)
   - Returns best available crop if no good match found
6. **Visualization**: Generates radar charts and confidence metrics
7. **Advice Generation**: Provides parameter-specific optimization tips

## Security Features

- Environment variables for sensitive configuration
- Secure filename handling for static assets
- Input validation and error handling
- Debug mode disabled in production
- CSRF protection via Flask sessions

## Performance

- **Model Accuracy**: 92%
- **Prediction Time**: < 100ms
- **Supported Crops**: 43+
- **Training Data**: Comprehensive soil-climate-crop dataset

## Future Enhancements

- Weather API integration for real-time climate data
- Soil testing kit integration
- Mobile app version
- Multi-language support
- Crop price predictions
- Pest and disease recommendations
- Irrigation scheduling

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or suggestions, please open an issue on GitHub or contact the development team.

## Contributors

- Development Team

---

**Last Updated**: 2024
**Version**: 1.0.0
