# Mars-CubeSat-Feasibility-ML
A Python-based feasibility study for a 12U CubeSat mission to Mars, featuring Hohmann transfer analysis and communication link budgeting.

# CubeSat Mission Concept: Mars Feasibility & ML Analysis 🛰️🔴

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Poliastro%20%7C%20Astropy-orange)
![ML](https://img.shields.io/badge/Machine%20Learning-Scikit--Learn-green)

## 📖 Project Overview
This project performs a preliminary feasibility study for a **12U CubeSat (24 kg)** mission to Mars. It utilizes physics-based modeling to simulate interplanetary transfer, communication link budgets, and power generation. 

Additionally, it integrates **Machine Learning (Random Forest Regressors)** to analyze how variations in mission parameters (antenna gain, solar efficiency) impact mission success metrics.

## 🎯 Objectives
* **Orbital Mechanics:** Model a Hohmann Transfer from Earth to Mars using `poliastro`.
* **Comms System:** Analyze the link budget using the Friis Transmission Equation (X-band).
* **Power Budget:** Assess solar power generation using an inverse-square law model.
* **ML Optimization:** Train a model on synthetic data to predict Received Power and Solar Output based on design constraints.

## 📊 Key Results

### 1. Trajectory Analysis (Hohmann Transfer)
* **Total Delta-V:** 5.588 km/s
* **Transfer Duration:** ~259 days
* **Interpretation:** The simulation confirms a plausible transfer window, though the Delta-V requirement suggests the need for a high-efficiency propulsion system or ride-share insertion.



[Image of Hohmann transfer orbit diagram]


### 2. Communication Link (X-Band)
* **Transmit Power:** 10 W (40 dBm)
* **Receiver Sensitivity Threshold:** -120 dBm
* **Result:** Signal strength drops significantly at Mars aphelion. The model indicates that a standard 10W transmitter with a 25dB gain antenna is marginal at maximum distance, requiring robust error correction or larger ground assets.

### 3. Machine Learning Analysis
We generated a synthetic dataset ($N=1000$) based on physics bounds to train a Random Forest Regressor.
* **Communication Model Accuracy ($R^2$):** 0.98
* **Power Model Accuracy ($R^2$):** 0.96
* **Feature Importance:** The model identified that **Distance** is the dominant factor for power generation (68% importance), while **Transmit Power** dominates the link budget (49% importance).

## 🛠️ Methodology & Tech Stack

### Physics Simulation
* **Libraries:** `poliastro`, `astropy`, `numpy`
* **Orbit:** Simplified circular coplanar orbits for Earth (1 AU) and Mars (1.52 AU).
* **Link Budget:** $P_r = P_t + G_t + G_r - L_{fs} - L_{misc}$

### Machine Learning
* **Libraries:** `scikit-learn`, `pandas`
* **Algorithm:** Random Forest Regressor (n_estimators=100).
* **Process:**
    1.  Generate synthetic data using physics constraints.
    2.  Preprocess and split data (80/20 train/test).
    3.  Train model to predict `Received_Power_dBm` and `Solar_Power_Output_W`.
    4.  Evaluate against physics ground truth.

## 🚀 Usage

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/@jafifa03/Mars-CubeSat-Feasibility-ML.git](https://github.com/your-username/Mars-CubeSat-Feasibility-ML.git)
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the analysis:**
    Open `notebooks/Mission_Feasibility_Analysis.ipynb` in Jupyter Lab or VS Code.

## 🔮 Future Work
* **Perturbations:** Incorporate J2 perturbations and third-body gravity using `poliastro`.
* **Real Data:** Integrate actual telemetry from the **MarCO** (Mars Cube One) mission for ML validation.
* **Thermal:** Add a thermal equilibrium model for eclipse periods.

## 📝 License

