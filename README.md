# risk analysis project

### Overview
This project focuses on calculating the Value at Risk (VaR) for a portfolio using different models: Parametric VaR, Monte Carlo VaR, and Historical VaR. The portfolio includes a payer (pay fixed leg) SOFR swap and $1 million investments in four stocks: AAPL, MSFT, F (Ford Motor), and BAC (Bank of America).

### Table of Contents

1. [Parametric VaR Model](#parametric-var-model)
2. [Monte Carlo VaR Model](#monte-carlo-var-model)
3. [Historical VaR Model](#historical-var-model)
4. [Results](#results)

### VaR Model Details

#### 1. Define the VaR Parameters
- **Significance Level**: 95%
- **Risk Horizon**: 1-day
- **Reporting Currency**

#### 2. Identify the Portfolio
- A payer (pay fixed leg) SOFR swap
- $1 million in each of the four stocks: AAPL, MSFT, F (Ford Motor), and BAC (Bank of America)

#### 3. Identify the Risk Factors of the Portfolio
- An interest rate curve
- Fluctuations in SOFR impacting the market value of swap transactions

#### 4. Model the Joint Distribution of the Risk Factors Over the Risk Horizon
- Parametric VaR
- Monte Carlo VaR
- Historical VaR

#### 5. Build the Distribution of the Portfolio P&L Over the Risk Horizon

#### 6. Calculate the VaR

---

### Prerequisites
- Python 3.x
- Pandas
- NumPy
- SciPy
- Matplotlib
- An Excel file containing historical data (`hist_data.xlsm`)

### Installation
1. Install the required Python libraries:
   ```sh
   pip install pandas numpy scipy matplotlib
   ```
2. Ensure the `hist_data.xlsm` file is in the same directory as the script.

### Usage
To run the VaR calculations, execute the script in a Python environment. The script will:
1. Clean and prepare the data.
2. Calculate VaR using different models.
3. Output the results.

### Data Cleaning
#### Swap Data
The SOFR curve data is loaded from an Excel sheet and transposed for further processing. The data is then converted to a datetime index.

#### Stocks Data
Historical data for the stocks AAPL, MSFT, F, and BAC is merged into a single DataFrame with adjusted closing prices.

### Parametric VaR Model
#### Swap
1. Calculate the discount factor.
2. Compute the present value (PV) of the fixed and floating legs.
3. Determine the weights and changes for VaR calculation.

#### Stocks
1. Calculate daily log returns for each stock.
2. Assign weights and compute the combined PV for stocks.

#### Combine
1. Merge the data for swaps and stocks.
2. Calculate mean and covariance.
3. Compute the Parametric VaR at the 95% confidence level.

### Monte Carlo VaR Model
#### Risk-based Approach
1. Simulate new changes using a multivariate normal distribution.
2. Calculate new portfolio values and sort the results.
3. Determine VaR using the simulated data.

#### Full Revaluation Approach
1. Simulate new data and compute new PV for swaps and stocks.
2. Combine the results to calculate the portfolio's value.
3. Determine VaR from the sorted values.

### Historical VaR Model
#### Risk-based Approach
1. Compute historical P&L based on changes in risk factors.
2. Sort the historical P&L data.
3. Determine VaR from the sorted historical data.

#### Full Revaluation Approach
1. Compute new PV for swaps and stocks using historical changes.
2. Combine the results to calculate daily P&L.
3. Determine VaR from the sorted P&L data.

### Results
The results of the VaR calculations are summarized in a DataFrame, showing the VaR values for each model:

```python
result_df = pd.DataFrame(columns=['VAR'])
result_df.loc['Para', 'VAR'] = VaR_parametric_95
result_df.loc['MC_fullre', 'VAR'] = VaR_MC_full_revaluation
result_df.loc['MC_riskbased', 'VAR'] = VaR_MC_risk_based_95
result_df.loc['Historical_fullre', 'VAR'] = VaR_historical_full_revaluation
result_df.loc['Historical_riskbased', 'VAR'] = VaR_historical_riskbased

print(result_df)
```



