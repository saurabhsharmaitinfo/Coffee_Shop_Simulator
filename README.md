# Coffee Shop Queue Simulation

## Overview
This project implements a discrete-event simulation of a coffee shop queue using **SimPy**, a Python library for modeling systems where events occur at specific points in time. The simulation models a coffee shop with 2 baristas, where customers arrive randomly (approximately every 3 minutes, following an exponential distribution) and are served for 3–7 minutes. It tracks wait times (time spent waiting for a barista) and queue lengths (number of customers waiting), producing statistics and visualizations to analyze the system’s performance.

The simulation runs in **Google Colab**, leveraging Python libraries like `simpy`, `numpy`, and `matplotlib` for computation and visualization. The code is robust, with error handling, synchronized data collection, and safeguards to prevent issues like array length mismatches or syntax errors.

## Features
- Simulates customer arrivals and service with 2 baristas.
- Tracks wait times and queue lengths.
- Computes statistics (average/max wait time, average queue length).
- Visualizes results with two `matplotlib` plots (wait times and queue lengths vs. time).
- Outputs data for optional Chart.js visualization.
- Includes error handling and parameter validation for reliability.
- Uses a random seed for reproducible results.

## Prerequisites
- **Google Colab**: The project is designed to run in a Google Colab notebook.
- **Python Libraries**:
  - `simpy`: For discrete-event simulation.
  - `numpy`: For statistical analysis.
  - `matplotlib`: For plotting results.
- No local installation is required, as libraries are installed in Colab.

## Setup Instructions
1. **Open Google Colab**:
   - Go to [Google Colab](https://colab.research.google.com/) and create a new notebook (`File > New Notebook`).
2. **Copy the Code**:
   - Paste the simulation code (provided below) into a single code cell in the Colab notebook.
3. **Run the Code**:
   - Press `Shift + Enter` to execute the cell.
   - The code automatically installs `simpy` and runs the simulation.
4. **Save the Notebook**:
   - Save to Google Drive (`File > Save`) or download as `.ipynb` (`File > Download > Download .ipynb`).

## Simulation Code
The complete code is available in the project repository or can be copied from the following description. Key components include:

- **Parameters**:
  - `RANDOM_SEED = 42`: Ensures reproducible results.
  - `SIM_TIME = 60`: Simulates 60 minutes.
  - `NUM_BARISTAS = 2`: Two baristas available.
  - `ARRIVAL_RATE = 1/3`: Customers arrive every ~3 minutes (exponential distribution).
  - `SERVICE_TIME_MIN = 3`, `SERVICE_TIME_MAX = 7`: Service time range.
  - `MAX_CUSTOMERS = 20`: Limits customers to ensure completion.
- **Functions**:
  - `customer`: Models a customer’s arrival, wait, and service.
  - `customer_generator`: Generates customers at random intervals.
  - `run_simulation`: Sets up and runs the SimPy environment.
  - `analyze_and_visualize`: Computes statistics and creates plots.
- **Output**: Console logs, statistics, and two `matplotlib` plots (wait times and queue lengths vs. time).

## Usage
1. **Run the Simulation**:
   - Execute the code cell in Colab.
   - Observe console output for customer events (e.g., `Customer0 arrived at 2.13, waited 0.00 minutes`), statistics (e.g., `Average wait time: 1.23 minutes`), and array lengths.
2. **View Plots**:
   - Two plots appear:
     - Left: Wait times vs. arrival times (blue line with markers).
     - Right: Queue lengths vs. arrival times (red line with markers).
3. **Chart.js Visualization**:
   - The code prints `Timestamps` and `Wait Times` for use in Chart.js.
   - Copy these values to create a custom Chart.js visualization (example provided below).
4. **Modify Parameters**:
   - Adjust `NUM_BARISTAS`, `ARRIVAL_RATE`, or `SIM_TIME` to simulate different scenarios (e.g., rush hours).
   - Rerun the cell to see updated results.

## Example Output
- **Console**:
  ```
  Customer0 arrived at 2.13, waited 0.00 minutes
  Customer0 served in 4.52 minutes, left at 6.65
  Customer1 arrived at 5.78, waited 0.00 minutes
  ...
  Generated 20 customers
  Average wait time: 1.23 minutes
  Maximum wait time: 4.56 minutes
  Average queue length: 0.45 customers
  Length of timestamps: 20, wait_times: 20, queue_lengths: 20
  Timestamps: [2.13, 5.78, 7.91, 10.45, 12.67, ...]
  Wait Times: [0.0, 0.0, 1.23, 2.45, 0.0, ...]
  ```
- **Plots**: Two `matplotlib` plots showing wait times and queue lengths over time.
- **Chart.js Example** (for external use):
  ```json
  {
    "type": "line",
    "data": {
      "labels": [2.13, 5.78, 7.91, 10.45, 12.67],
      "datasets": [{
        "label": "Wait Times (minutes)",
        "data": [0.0, 0.0, 1.23, 2.45, 0.0],
        "borderColor": "#2196F3",
        "backgroundColor": "rgba(33, 150, 243, 0.2)",
        "fill": true,
        "pointRadius": 5
      }]
    },
    "options": {
      "scales": {
        "y": { "beginAtZero": true, "title": { "display": true, "text": "Wait Time (minutes)" } },
        "x": { "title": { "display": true, "text": "Time (minutes)" } }
      },
      "plugins": { "legend": { "display": true } }
    }
  }
  ```

## Troubleshooting
- **No Output/Plots**: Ensure `!pip install simpy` ran successfully and `MAX_CUSTOMERS`/`SIM_TIME` are reasonable (e.g., 20 and 60).
- **Array Length Mismatch**: Unlikely, but the code trims arrays if needed and prints a warning.
- **Unexpected Results**: Verify `ARRIVAL_RATE = 1/3` and `random.seed(42)` for consistency.
- **Errors**: Check console for error messages (e.g., invalid parameters).

## Extending the Project
- **Priority Customers**: Use `simpy.PriorityResource` to model VIP customers.
- **Inventory**: Add `simpy.Container` for coffee bean inventory.
- **Export Data**: Save results to CSV with `pandas`:
  ```python
  import pandas as pd
  pd.DataFrame({"Time": timestamps, "Wait": wait_times}).to_csv("results.csv")
  ```
- **Test Scenarios**: Vary `NUM_BARISTAS` or `ARRIVAL_RATE` to simulate
