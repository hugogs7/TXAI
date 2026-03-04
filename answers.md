### Question 1

**Select the adversarial debiasing report and answer: What does it mean Conditioned Demographic Parity in this context?**

**Answer:**
In the context of the Aequitas adversarial debiasing report, **Conditioned Demographic Parity** is a fairness metric that evaluates whether the model's predicted outcomes (in this case, the decision to "Pass" or "Not Pass") are distributed equally across different groups of a sensitive attribute (which is "socioeconomic_status" in this report). 

Specifically, it measures the disparity in the proportion of a specific outcome received by different demographic groups (e.g., High SES vs. Low SES students). If Conditioned Demographic Parity is achieved (value at or near 0), it means the model is not favoring one socioeconomic group over another when predicting who will pass or fail. 

### Question 2

**What is the significance of High socioeconomic status (SES) students showing a positive value while Low SES students show a negative value within this specific category?**

**Answer:**
Looking at the Conditioned Demographic Disparity charts for the "Pass" decision, High SES shows a positive bar while Low SES shows a negative bar. 

The significance of this is that it highlights a clear bias or disparity in the outcomes:
**Positive value (High SES):** This means that students with a high socioeconomic status are overrepresented in the positive outcome ("Pass") relative to the overall average. 
**Negative value (Low SES):** This indicates that students with a low socioeconomic status are underrepresented, receiving the "Pass" outcome at a lower rate than the baseline. 

In short, it signifies that the model (or the historical data it learned from) favors the privileged group (High SES) and disadvantages the vulnerable group (Low SES) for successful academic outcomes.

### Question 3

**Do you notice any difference in performance and fairness metrics after applying the adversarial debiasing model?**

**Answer:**
No, there is absolutely no noticeable difference in either the performance or the fairness metrics after applying the adversarial debiasing technique. 

* **Performance Metrics:** When analyzing the "Performance Plot," the metrics for Accuracy, Precision, Recall, ROC AUC, and F1 remain completely unchanged. In both the baseline ("No Mitigation") and the post-intervention ("With Mitigation") scenarios, all performance metrics sit at a perfect 1.0.
* **Fairness Metrics:** Similarly, the "Fairness Plot" shows zero changes. The Demographic Parity Ratio remains stagnant at approximately 0.68, and the Equalized Odds Ratio remains at 1.0 in both scenarios. 

In conclusion, for this specific dataset and configuration, the adversarial debiasing mitigation technique had no impact. It neither harmed the model's predictive power nor helped reduce the existing demographic disparity.

### Question 4

**If you had to evaluate the model's performance by subgroups of a sensitive attribute, which metric do you think is not susceptible to the decision threshold? Why is this important?**

**Answer:**
Among the performance metrics typically evaluated in these fairness reports (such as Accuracy, Precision, Recall, ROC AUC, and F1), the metric that is not susceptible to the decision threshold is the **ROC AUC** (Receiver Operating Characteristic - Area Under the Curve).

**Why is this important?**
Most standard metrics (like Accuracy, Precision, and Recall) require a fixed decision threshold (e.g., setting a 0.5 cutoff) to classify a continuous probability into a discrete "Pass" or "Not Pass" outcome. 

The ROC AUC is important because it measures the model's ability to rank positive instances higher than negative instances across *all* possible classification thresholds. When evaluating subgroups of a sensitive attribute, using ROC AUC is crucial for two main reasons:
1. **Assessing inherent predictive power:** It tells you if the model is fundamentally able to distinguish between positive and negative outcomes for a specific disadvantaged group, regardless of where the cutoff point is set.
2. **Identifying threshold-related bias:** If a model has low accuracy but a high ROC AUC for a vulnerable subgroup, it means the model's internal scoring is actually fine, but the chosen global threshold is misaligned for them. Conversely, a low ROC AUC indicates a deeper issue: the model's features or training are failing to properly represent and score that subgroup entirely.