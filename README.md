# Stock-Price-Prediction
# 📈 LSTM-Based Stock Price Prediction

This project demonstrates how to use an **LSTM (Long Short-Term Memory)** neural network to predict future stock prices based on historical data. It takes past stock prices as input and generates predicted prices step-by-step.

---

## 📊 Dataset

- **Source**: CSV file of historical stock prices.
- **Format**: Date, Open, High, Low, Close, Volume, etc.
- **Used Feature**: `Close` price (can be customized)

---

## 🧠 What This Project Does

- Loads historical stock price data  
- Scales the data using MinMaxScaler  
- Creates input-output sequences for training  
- Builds and trains an LSTM model  
- Predicts future prices step-by-step using the last window  
- Prints 100-step future forecast

---

## 🔧 Libraries Used

- `numpy`
- `pandas`
- `matplotlib`
- `scikit-learn`
- `tensorflow / keras`

⚙️ Project Workflow

1. Data Preparation
      Load CSV data using pandas
      Extract the Close prices
      Normalize with MinMaxScaler
      Create input sequences of fixed length (e.g., 100)

2. Model Building
      Build an LSTM model with input shape (n_steps, 1)
      Add Dense output layer for 1-step prediction

3. Training
      Train on the scaled data using past 100 time steps as input
      Use MSE loss and Adam optimizer

4. Prediction Loop
      Start with last 100 values from test data
      For each future day:
            Predict next value
            Append it to input
            Drop the oldest value to maintain input length
      Repeat for 100 steps
   

🔮 Sample Prediction Loop

lst_output2 = []
n_steps2 = 100
i = 0

while i < 100:
    if len(temp_input) > 100:
        x_input = np.array(temp_input[1:])
        x_input = x_input.reshape((1, n_steps2, 1))
        yhat = model.predict(x_input, verbose=0)
        temp_input.extend(yhat[0].tolist())
        temp_input = temp_input[1:]
        lst_output2.extend(yhat.tolist())
        i += 1
    else:
        x_input = np.array(temp_input).reshape((1, n_steps2, 1))
        yhat = model.predict(x_input, verbose=0)
        temp_input.extend(yhat[0].tolist())
        lst_output2.extend(yhat.tolist())
        i += 1

        
📈 Example Output

0 day output: [[150.32]]
1 day output: [[150.67]]
2 day output: [[151.02]]
...
100 day output: [[170.25]]


📌 Future Improvements
    
    Use multi-feature inputs (Open, High, Low, Volume)
    Add moving averages as features
    Add real-time prediction with live stock data
    Deploy using Flask or Streamlit for user input


