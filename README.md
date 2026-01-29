# Traffic Prediction & Route Optimization

This project implements an intelligent traffic prediction and route optimization system for San Francisco. It combines historical traffic data analysis, machine learning (Random Forest Regressor), and real-time news updates to predict traffic flow and determine the optimal route between two locations.

## 🚀 Key Features

*   **Traffic Flow Prediction**: Uses a **Random Forest Regressor** to forecast traffic density based on historical PeMS (CalTrans) data. The model achieves an $R^2$ score of **0.87**.
*   **Smart Routing**: Implements **Dijkstra's Algorithm** to calculate the shortest path, dynamically adjusting edge weights based on predicted traffic and active road incidents.
*   **Real-time Context**: Integrates **NewsAPI** to fetch real-time reports on accidents, protests, and lane closures, updating route costs accordingly.
*   **Interactive Visualization**: Generates dynamic maps using **Folium** to visualize the optimal path and traffic conditions.

## 📂 Project Structure

- **`ETL.ipynb`**: Extract, Transform, Load. Cleans raw PeMS data, handles missing values, and prepares the dataset for analysis.
- **`EDA.ipynb`**: Exploratory Data Analysis. Visualizes traffic patterns over time to understand peak hours and weekly trends.
- **`ML.ipynb`**: Machine Learning. Trains the Random Forest Regressor on the processed data and saves the model (`rf.pkl`).
- **`Final project.ipynb`**: The main application interface.
    - Loads the trained model.
    - Fetches real-time traffic news.
    - runs the Dijkstra optimization.
    - Outputs the final route map (`output.html`).
- **`rf.pkl`**: Serialized trained Random Forest model.
- **`output.html`**: Generated map file showing the optimal route.

## 🛠️ Prerequisites

Ensure you have the following Python libraries installed:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn joblib requests folium geopy beautifulsoup4
```

## ⚙️ Setup & Usage

1.  **Data Preparation**:
    *   Run `ETL.ipynb` to process the raw traffic data.
    *   Run `EDA.ipynb` if you wish to inspect data visualizations.

2.  **Model Training**:
    *   Run `ML.ipynb` to train the prediction model. This will generate the `rf.pkl` file (pre-trained model is already included).

3.  **Run the Application**:
    *   Open `Final project.ipynb`.
    *   Ensure you have a valid **NewsAPI Key** in the `newsapi` function.
    *   Run all cells. You will be prompted to enter a **Start Location** and **End Location** (e.g., "Databricks" to "Hyatt").
    *   The notebook will calculate the best path and save it to `output.html`.

4.  **View Results**:
    *   Open `output.html` in your web browser to see the interactive map with the plotted route.

## 🧠 Methodology

1.  **Data**: We use 5-minute interval traffic flow data from CalTrans (District 12).
2.  **Prediction**: A Random Forest model predicts traffic flow for specific road segments given the time and day of the week.
3.  **Graph Construction**: The map is represented as a graph where nodes are intersections/locations and edges are streets.
    *   *Base Weight*: Physical distance.
    *   *Dynamic Weight*: Adjusted based on ML traffic predictions and NewsAPI incidents (e.g., an accident doubles the cost of an edge).
4.  **Optimization**: Dijkstra's algorithm traverses this dynamic graph to find the path with the lowest cost (travel time).

## 📊 Performance

*   **Model Accuracy**: $R^2 = 0.87$
*   **Latency**: Predictions and routing are computed in near real-time.

---
*Note: This project is meant for educational and research purposes.*
