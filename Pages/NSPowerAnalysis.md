## ⚡ Nova Scotia Power Pilot Analysis

**Background Information:**  
This project evaluates the impact of **insulation retrofits** on residential electricity consumption using advanced statistical methods. By combining **Pair Matching** and **Difference-in-Differences (DiD)** techniques, the study quantifies household energy savings, cost reductions, and GHG emission impacts. The analysis highlights the potential of data-driven energy efficiency programs in shaping Nova Scotia’s sustainable future. 📉🌱⚡

---

### Technology Used

<table>
  <tr>
    <td>🔹 Python (EDA, Cleaning, Pair Matching, DiD Estimation)</td>
    <td>🔹 Power BI (Interactive Reporting & Visualization)</td>
  </tr>
</table>

---

### 🐍 Python Workflow

Python was the backbone of data preparation and analysis:  
- **Data Cleaning & EDA:** Removed outliers, handled invalid dates, and standardized datasets.  
- **Pair Matching:** Applied **PCA + correlation/distance metrics** to match treatment homes (with insulation retrofits) to control homes.  
- **Difference-in-Differences (DiD):** Estimated the insulation effect by comparing matched treatment-control pairs before and during the pilot.  
- **Outputs:** Exported matched pairs, daily load profiles, monthly comparisons, and savings estimates for further visualization.  

[![Python Analysis Scripts](/images/NSP_Pilot/Python_Workflow.png?raw=true)](/images/NSP_Pilot/Python_Workflow.png?raw=true)

---

### 📊 Data Preparation & Workflow

1. **Raw Data:** Smart meter Excel files (pre- and during-pilot).  
2. **Cleaning:** Outlier removal (e.g., -437 kWh & 100,098 kWh), invalid leap day removed, duplicates handled.  
3. **Integration:** Combined Part A (Pre-Pilot) and Part B (During Pilot) for unified DiD analysis.  
4. **Pair Matching:** Created treatment-control pairs based on annual consumption profiles.  
5. **Impact Evaluation:** Performed DiD analysis to estimate insulation effect.  
6. **Validation:** Charts, plots, and CSVs generated for diagnostic checks.  
7. **Cost & GHG Reference:** Translated savings into **household bill impacts** and **emissions reductions**.  

---

### 🔎 Matching Analysis (Part A)

<iframe src="/pdf/NSPowerAnalysis/PartAPlots/PartA_Plots.pdf" width="100%" height="600px"></iframe>

**Key Insights**  
- 📊 Strong **seasonal alignment** observed between treatment and control groups.  
- ✅ High-quality matches achieved with **correlation > 0.9** for many pairs.  
- ⚠️ Outliers and mismatches were flagged for further **review and refinement**.  

---

### 📉 Difference-in-Differences (Part B)

[![DiD Analysis Results](/images/NSP_Pilot/DiD_Analysis.png?raw=true)](/images/NSP_Pilot/DiD_Analysis.png?raw=true)

- **Treatment Group:** Consumption rose slightly post-pilot.  
- **Control Group:** Consumption rose more steeply.  
- **DiD Estimate:** Net savings of ~**6% reduction in electricity consumption**.  
- Demonstrates **clear benefits of insulation retrofits** in reducing household load.  

---

### 🌍 Cost & Environmental Benefits

[![Cost & GHG Analysis](/images/NSP_Pilot/Cost_GHG.png?raw=true)](/images/NSP_Pilot/Cost_GHG.png?raw=true)

- **Cost Savings:** Lower household bills through reduced energy use.  
- **GHG Reductions:** Measurable decrease in emissions aligned with Nova Scotia’s climate goals.  
- **Grid Reliability:** Reduced strain during peak demand hours.  

---

### 📈 Power BI Dashboard

[![Power BI NSP Pilot Report](/images/NSP_Pilot/NSP_Pilot_Report.png?raw=true)](/images/NSP_Pilot/NSP_Pilot_Report.png?raw=true)

- **Interactive dashboards** with hourly, monthly, and seasonal consumption views.  
- **Segmentation** by treatment group and pilot phase (Pre vs During).  
- **Embedded DiD analysis** for intuitive exploration of program impacts.  

---

## 📝 Conclusion

The Nova Scotia Power Pilot demonstrates that **insulation retrofits reduce household electricity consumption by ~6%**, directly translating into **cost savings and GHG reductions**. With a structured workflow combining Python analytics and Power BI reporting, the project delivers transparent, data-driven insights. These findings not only validate the pilot’s effectiveness but also provide a strong foundation for **scaling energy efficiency programs**, supporting **sustainability, resilience, and long-term community benefits**. ⚡🌱📊
