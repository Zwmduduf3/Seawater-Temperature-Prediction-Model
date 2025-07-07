# Surface Temperature Forecasting using Linear Basis Function Models
# 基于线性基函数模型的海洋表面温度预测

## Project Background / 项目背景

Climate change is one of the most pressing global challenges of our time. As part of the UN Sustainable Development Goals (Goal 13: Climate Action), accurate forecasting of surface air temperature plays a vital role in understanding long-term climate trends and informing policy decisions. This project builds a statistical learning model to predict future surface temperatures using historical monthly data collected from 1940 to 2024.

气候变化是当今全球最紧迫的问题之一。根据联合国可持续发展目标（第13条：气候行动），准确预测地表空气温度对于理解气候趋势、制定环境政策具有重要意义。本项目基于1940年至2024年的历史月度数据，构建线性基函数回归模型，用于预测未来海洋表面温度。

## Project Objective / 项目目标

This project investigates the predictive performance of three families of basis functions under a Linear Basis Function (LBF) regression framework:

本项目旨在比较以下三类基函数在 LBF（线性基函数）模型中的预测能力：

- **Polynomial basis functions / 多项式基函数**
- **Piece-wise constant basis functions / 分段常数基函数**
- **Piece-wise linear basis functions / 分段线性基函数**

The model with the lowest test Mean Squared Error (MSE) will be selected to forecast ocean surface temperatures for **October, November, and December 2024**.

通过验证集选择最优超参数后，比较三类模型在测试集上的 MSE，最终使用最佳模型对 **2024年10月、11月和12月的气温** 进行预测。

## 📊 Dataset / 数据集信息

- Source: [ERA5 Surface Air Temperature Dataset](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5)
- Records: 1,017 monthly observations
- Time span: January 1940 – September 2024
- Features:
  - `year`: Year of observation / 观测年份
  - `month`: Month of observation / 观测月份
  - `temp`: Monthly average surface temperature (°C) / 平均表面气温（摄氏度）

## 🧠 Methodology / 方法概述

The LBF model is defined as:

> 𝑦 = 𝐮ᵀα + ϕ(x)ᵀβ + ε

Where:

- 𝑦 is the observed temperature  
- 𝐮 is a vector of month dummy variables  
- ϕ(x) represents the basis function transformations of year `x`  
- α and β are learnable parameter vectors  
- ε is the error term  

### Model families and basis functions:

1. **Polynomial**: ϕ(x) = [x¹, x², ..., x^p]
2. **Piece-wise Constant**: Indicator-based segmented constant functions
3. **Piece-wise Linear**: Piece-wise linear splines: (x - tᵢ) * I(x > tᵢ)

### Hyperparameter Selection:

- Polynomial: degree `p ∈ [1, 10]`
- Piece-wise: breakpoints `k ∈ [1, 30]`
- Selection criterion: minimum validation set MSE

## Results / 实验结果

| Model Type / 模型类型        | Optimal Param / 最优参数 | Test MSE |
|------------------------------|----------------------------|----------|
| Polynomial                   | p = 2                      | 0.0232   |
| Piece-wise Constant          | k = 24                     | 0.0206   |
| Piece-wise Linear            | k = 27                     | **0.0180** ✅ |

Piece-wise linear model achieved the lowest MSE and was selected for prediction.

分段线性模型的测试误差最小，因而被选为最终预测模型。

### 📈 2024 Q4 Predictions / 2024年第四季度气温预测：

| Month / 月份     | Predicted Temp (°C) / 预测气温 |
|------------------|-------------------------------|
| October / 十月   | 13.92                        |
| November / 十一月| 14.18                        |
| December / 十二月| 14.86                        |


