# Interest Rate Prediction with CIR Model

## What's This About?

Ever wondered if you could predict all interest rates just by knowing one of them? This project tries to do exactly that using the **Cox-Ingersoll-Ross (CIR) model**, which is what finance people use to model interest rates.

The idea is simple: given the 3-month rate, can we predict the full yield curve (6M, 1Y, 2Y, etc.)? Spoiler: mostly yes, but the 2-year is tricky.

## What You'll Find Here

- **CIR Model**: Standard interest rate model with mean-reverting dynamics
- **CIR++ Extension**: Added a smart trick to match the real market curve better
- **Full Validation**: Tested everything - sensitivity analysis, stress scenarios, cross-validation
- **Jupyter Notebook**: All code and explanations in one place

## How to Use It

1. **Install dependencies**:
   ```bash
   pip install numpy pandas scipy scikit-learn matplotlib seaborn
   ```

2. **Run the notebook**:
   - Open `CIR_Project.ipynb` in Jupyter
   - Run cells in order (Part 1 through 13)

3. **Data**:
   - Training data: `data/train_data.csv` (1000+ daily observations)
   - Test data: `data/test_data.csv` and `data/test_data_3M.csv`

## Key Results

| Maturity | RMSE (%) | R² Score | Notes |
|----------|----------|----------|-------|
| 6 Month  | 0.006    | 0.92     | Fits well ✓ |
| 1 Year   | 0.008    | 0.85     | Pretty good |
| 2 Year   | 0.012    | 0.58     | Tricky one |

**Bottom line**: The model works great for shorter maturities. The 2Y yield needs extra factors to predict well (single-factor models have limits).

## What's Inside Each Part

1. **Setup & Data Loading** - Get the raw data ready
2. **Model Theory** - Math behind CIR and mean reversion
3. **Calibration** - Fit parameters to historical data
4. **Predictions** - Forecast the test period yields
5. **Performance Metrics** - How accurate were we?
6. **Visual Comparisons** - Charts and plots
7. **CIR++ Extension** - Better curve fitting
8. **Advanced Analysis** - Spread dynamics, rolling forecasts
9. **Robustness Checks** - Daily vs weekly calibration
10. **Model Limitations** - When it breaks down
11. **Discussion** - What we learned
12. **Advanced Diagnostics** - Feller condition, stress tests, cross-validation
13. **Summary** - Direct answers to research questions

## Did It Actually Work?

**The good:**
- ✓ Robust calibration (parameters stable across different starting points)
- ✓ No overfitting (cross-validation confirms generalization)
- ✓ Mean reversion makes sense (shocks fade in ~3-4 months)
- ✓ Model survives stress periods (errors only rise 1.5x in high volatility)

**The limitations:**
- ⚠ Single-factor model can't explain all long-term rate movements
- ⚠ 2Y yield needs a second factor or regime-switching approach
- ⚠ Assumes normally distributed rates (small gaps near zero)

## Technical Notes

- **Calibration Method**: Quasi-MLE with L-BFGS-B optimizer
- **Time Step**: Daily (1/252 year)
- **Bond Pricing**: Uses closed-form affine solution
- **Validation**: 5-fold cross-validation on training data

## Key Insight

If you're managing interest rate risk, CIR++ is production-ready for hedging vanilla bonds. For derivatives pricing or tail-risk products, consider CIR-Jump for crisis scenarios. For the longest maturities, you'll want a second factor.

## Questions Answered

This project directly addresses 9 core research questions about:
- Calibration robustness
- Prediction accuracy by maturity
- Systematic bias patterns
- Whether extensions actually help
- Jump processes in crisis periods
- Parameter stability over time

