# Forecasting Future Realized Volatility

Final project for the Erdos Spring 2026 Quant Finance Bootcamp.

This project studies future realized volatility forecasting for a panel of 55 U.S. equities and ETFs using daily OHLCV data from 2016 to 2025. The target is the next 5-day annualized realized volatility. I compare a classical financial baseline, tree-based machine learning models, and sequence models on the same forecasting task.

## Project Summary

The feature set combines stock-level volatility, range, and volume signals with market, macro, and credit proxies such as `SPY`, `QQQ`, `IWM`, `^VIX`, Treasury yields, `HYG`, and `LQD`.

The first benchmark is a HAR-RV model, which provides a clean and interpretable financial baseline. On the 2025 test set it achieved:

- `RMSE = 0.1709`
- `MAE = 0.1010`

The next step is XGBoost, which uses a richer tabular feature set to model nonlinearities and feature interactions. Pure XGBoost improved performance to:

- `RMSE = 0.1598`
- `MAE = 0.0951`

To test whether a sequence model could still add local timing information, I also built a hybrid XGBoost + residual TCN model. This hybrid produced the best overall result in the final cleaned comparison:

- `RMSE = 0.1584`
- `MAE = 0.0939`

I also compared transformer-based sequence models. The baseline transformer underperformed the tabular models, and a tuned transformer improved noticeably, but still did not beat the XGBoost-based models.

Overall, the main empirical conclusion is that future realized volatility is a much more stable and meaningful target than price prediction for this kind of comparison, and that tree-based nonlinear models remain the strongest choice on this daily panel forecasting problem.

## Repository Structure

- `01_data_download_and_features.ipynb`: data loading, cleaning, and feature engineering
- `02_har_rv_baseline.ipynb`: HAR-RV benchmark model
- `03_xgboost_and_hybrid.ipynb`: XGBoost and XGBoost + residual TCN results
- `04_transformer_baseline_and_tuned.ipynb`: baseline and tuned transformer results
- `figures/`: main plots used in the final presentation
- `artifacts/`: saved model weights, pipelines, and metadata
- `presentation/`: compiled PDF files for the summary and slides
- `archive/`: additional experiments and intermediate model variants that were not kept in the final mainline workflow

## Presentation Files

- `presentation/Project_Summary.pdf`
- `presentation/Volatility_Project_Slides.pdf`

## Notes

Large raw and processed data files are intentionally excluded from GitHub. The repository keeps the notebooks, figures, and saved model artifacts needed to understand and reproduce the main modeling workflow.
