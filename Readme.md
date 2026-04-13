# Traffic Monitoring AI

This project loads a Sumo traffic simulation network and then trains a neural network that
predicts the speed of a vehicle in the next time step based on:
    - the speed of the vehicle in the current time step, 
    - the distance between the vehicle and the leading vehicle in the current time step
    - the speed of the leading vehicle in the current time step 

Then it colors the streets according to the predicted speed in the next time step

**code is private For code access or questions, please contact me at: tst1880@googlemail.com**

<br>
<br>
<br>

## Libraries used 
- traci
- numpy 
- pandas
- scikit-learn
- matplotlib

## Use Case

The goal is to explore whether simple ML models can anticipate short‑term traffic dynamics and support congestion analysis

This has significant potential for future data‑driven traffic management systems 

<br>
<br>
<br>

## Project Structure
- `get_data.py`: Running the sumo traffic simulation and gathering training data
- `training.py`: Script for training the neural network model
- `testing.py`: Script for evaluating model performance

<br>
<br>
<br>

### get_data.py

```mermaid

flowchart TD

A[run Simulation city_center.sumocfg] --> B[store trainingsdata in X.npy and y.npy]

```

X is an array that contains:
- the speed of the vehicle in the current time step, 
- the distance between the vehicle and the leading vehicle in the current time step
- the speed of the leading vehicle in the current time step 

y is an array that contains:
- speed at the next time step 

<br>
<br>
<br>

### training.py

```mermaid

flowchart TD

A[load X.npy and y.npy] --> B[split X and y in trainings and testdata]
B --> C[train neural network]
```

<br>
<br>
<br>

#### Results form training 

<img src="./results/training_results.png" width="600">

- R² = 0.94 — the model explains 94% of the variance in vehicle speeds, meaning it can predict speeds reliably across a wide range of traffic conditions.

- MAE = 2.34 km/h — the mean absolute error is low, indicating that the predicted speeds are very close to the actual speeds.

- Both metrics confirm the model’s accuracy, which is also visible in the scatter plot where most points lie close to the angle bisector (red line).


### testing.py 


```mermaid

flowchart TD

A[load neural network] --> B[load Simulation city_center_2.sumocfg]
B --> C[run Simulation] 
C --> D[make prediction for next time step]
D --> E[Simulation ends]
E --> F[calculate the mean of the predicted speed for every lane at every time step]
F --> G[save every frame in the frames folder]
```
<br>
<br>
<br>

## Results

- below is the result, the frames are converted to a gif

### Legend
- red: Neural Network predicts mean speeds below 10 km/h for the lane 
- yellow: Neural Network predicts mean speeds between 10 km/h and 20 km/h for the lane 
- green: Neural Network predicts mean speeds above 30 km/h for the lane 

<img src="./results/result.gif" width="600">




