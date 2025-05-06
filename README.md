## 📊 Dataset 1: `summary_and_regression_data.csv`

This dataset was used for:

- **Generating summary statistics** (see Table 1 of the manuscript)
- **Fitting linear regression models** to analyze the effects of fuel treatments, vegetation, ignition, and weather variables on:
  - Area burned (AB)
  - Total cost (TC), including fuel treatment and timber loss due to wildfire

The variables included in this dataset are described in **Table 1** of the manuscript.  
Note: While **air temperature is listed in Celsius (`T_inC`)** in Table 1 for clarity, the **regression models use temperature in Kelvin (`T_inK`)** to improve numerical stability and interpretability.

All continuous response variables were log-transformed (`log_AB` and `log_TC`) to meet model assumptions.

---

### 📈 Example R Code for Regression Models

#### 🔹 Area Burned Model (Results in Table 2)

```r
model_ab <- lm(log_AB ~ h + RH + WS + T_inK + PB + TFB + Bdtn + Bdnt + Bm + tau +
                  PB:Bdtn + PB:Bdnt + TFB:Bdtn + TFB:Bdnt +
                  PB:Bm + TFB:Bm + PB:tau + TFB:tau + PB:d + TFB:d,
               data = data_summary_regression)
summary(model_ab)
```

#### 🔹 Total Cost Model (Results in Table 3)

```r
model_tc <- lm(log_TC ~ h + RH + WS + T_inK + PB + TFB + Bdtn + Bdnt + Bm + tau +
                  PB:Bdtn + PB:Bdnt + TFB:Bdtn + TFB:Bdnt +
                  PB:Bm + TFB:Bm + TFB:tau + PB:d,
               data = data_summary_regression)
summary(model_tc)
```

> **Note**:  
> - Regression results for the area burned and total cost models are presented in **Tables 2 and 3** of the manuscript.  
> - The **estimated coefficients from these models** were also used to visualize marginal effects in **Figures 4 and 5**.

## 📊 Dataset 2: `FARSITE_outputs.csv`

This dataset was used for:

- **Creating bar charts** that visualize the effects of fuel treatments on wildfire behavior and cost-related outcomes under various simulation scenarios.
- Specifically, it was used to generate:
  - **Figure 3** in the main manuscript
  - **S3 and S4 Figs of supporting information**

Each row in the dataset represents a summary of FARSITE simulation outputs under a specific combination of treatment, location, and fire behavior context. The dataset includes mean values and corresponding **95% confidence intervals** for the following wildfire outcome variables:

- Area burned (AB)
- Total cost (TC)
- Crown fire activity (CFA)
- Fireline intensity (FI)
- Flame length (FL)
- High potential underburn area (HPUA)
- Rate of spread (ROS)
- Residence time (RI)

The dataset was derived by aggregating the outputs of multiple FARSITE runs (excluding ignition scenario Q0 and filtering for the final hour of simulation), and was used exclusively for visualization, not for statistical modeling.

> **Note**: Bar charts in **Figure 3** and **S3 and S4 Figs of supporting information** were generated using the mean and 95% CI values in this dataset.

