# 🐅 Tiger Movement Prediction with Zone Classification and Red Zone Visualization


Team Memebers  
Rudra Saini - 500109466  AIML B2  
Ashutosh Pant - 500109916 AIML B2

This project predicts the possible future location zone of a tiger in the Jim Corbett sanctuary based on historical GPS data, temperature, and timestamp features. Additionally, it visualizes high-risk ("Red Zone") areas based on clustering patterns in past movements.

---

## 📋 Why Synthetic Data?

Due to the lack of access to real-time GPS and ecological tiger tracking datasets, **synthetic data** was created to:

- Simulate real-world tiger movements across known zones.
- Maintain geographic and temporal plausibility.
- Enable model training, testing, and visualization with full control over variables.

The synthetic dataset includes:

- Date and time of sighting  
- Tiger ID (e.g., Tiger1, Tiger2, Tiger3)  
- GPS coordinates (latitude and longitude)  
- Temperature at the time of sighting  
- Manually labeled `LocationZone`  

---

## 🛠 Features & Technologies

| Component       | Purpose                                          |
|----------------|--------------------------------------------------|
| `pandas`        | Data processing                                  |
| `sklearn`       | Random Forest classifier and KMeans clustering   |
| `matplotlib`    | Plotting sanctuary map and tiger locations       |
| `datetime`      | Feature extraction from time inputs              |
| `LabelEncoder`  | Encoding target labels for supervised learning   |

---

## 🔁 Step-by-Step Data Processing

### ✅ Load Data
The synthetic CSV is embedded in the code using `StringIO`, simulating an internal dataset.

### 🔧 Feature Engineering
Datetime features are extracted from the `Date` and `Time` columns:

- `Datetime` → converted from `Date` + `Time`
- Extracted features:
  - `Hour` of day
  - `DayOfWeek` (0=Monday, 6=Sunday)
  - `Month`

### 🎯 Feature Selection for Model Training
**Inputs (X):**

- Latitude (`LastSeenLatitude`)
- Longitude (`LastSeenLongitude`)
- Temperature
- Hour of day
- Day of the week
- Month

**Output (y):**

- `LocationZone` (encoded using `LabelEncoder`)

---

## 🤖 Model Training

A `RandomForestClassifier` is trained using the above features to predict the `LocationZone`, i.e., where a tiger might be found based on its latest position, temperature, and the given time.

---

## 🌲 Why Random Forest?

Random Forest is a robust ensemble learning technique ideal for this problem because:

- It handles both numerical and categorical features.
- It captures complex, non-linear relationships.
- It’s less prone to overfitting due to its bagging mechanism.

This makes it effective for predicting future tiger zones using patterns from GPS data, time, and weather.

---

## 📍 Post-Prediction: KMeans for Red Zone Clustering

Once the probable zone is predicted:

1. Past latitude/longitude points of the selected tiger are clustered using **KMeans** (3 clusters).
2. The **cluster centers** represent historically visited hotspots.
3. The nearest cluster center to the predicted zone is marked as the **Red Zone**.

> 🧠 **Note:** KMeans is **not used** for prediction, but rather for visualizing spatial patterns — useful for park rangers or conservationists to identify areas of frequent tiger activity.

---

## 🗺 Visualization

- The sanctuary map (`jim corbett.jpeg`) is loaded using `matplotlib`.
- Zones from `zone_coords` are plotted in **blue**.
- The **predicted location** is shown in **red triangle**.
- The **nearest cluster center** (frequently visited area) is shown in **green**, surrounded by a **red circle labeled “Red Zone”**.

---
