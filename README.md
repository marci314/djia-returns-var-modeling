# In-Sample Modeling and 1% Value-at-Risk for DJIA Stocks

### Overview
This project fits several parametric models to daily percentage log-returns of 25 DJIA stocks using Maximum Likelihood Estimation (MLE). It compares models using AIC/BIC and evaluates their accuracy in estimating 1% Value-at-Risk (VaR).

### Implemented Models
* **Gaussian**: $X \sim N(\mu, \sigma^2)$.
* **Mixture of Gaussians (MoG)**: Fits 2 and 3 components to capture non-normal features such as heavier tails and higher peaks.
* **Weighted Sum of $\chi_1^2$ Variables**: $X = \mu + \sum_{j=1}^{K} a_j C_j$. The PDF is computed via numerical inversion of the characteristic function.
* **Location-Scale Non-Central $t$ (NCT)**: $Y = \mu + \sigma T$, where $T$ follows a non-central t distribution.

### Key Findings
* **Model Selection**: The NCT model is frequently selected as the best fit by the BIC criterion due to its balance of flexibility and parsimony with 4 parameters.
* **Risk Estimation**: Gaussian models consistently underestimate left-tail risk because the normal distribution fails to account for the heavy tails typically present in daily stock returns.
* **Tail Behavior**: MoG and NCT models generally provide VaR estimates closer to the empirical sample VaR by allowing for heavier tails through high-variance components or specific degrees-of-freedom parameters.

### Implementation Details
* **Software**: All numerical work, including MLE optimization and VaR calculation, was conducted in **MATLAB R2024b**.
* **Optimization**: The project uses `fminsearch` for Gaussian, MoG, and NCT models, and `mle` with custom likelihoods for the weighted $\chi^2$ model.
