# Machine-Learning-Challenge
# The Logistics Auditor

## A. Executive Summary

Veridi Logistics (Olist) experiences late deliveries in approximately 8–12% of orders overall, with Northeastern and Northern states showing significantly higher rates (e.g., AL 20.8%, MA 17.1%, SE 15.0%) compared to SP (~3–5%). Late and especially Super Late deliveries strongly correlate with poor customer reviews (average scores of 3.0 and 1.7 respectively, versus 4.3 for On Time), confirming that inaccurate estimated delivery dates are a major driver of negative sentiment and potential customer churn. A simple neural network was built to predict the risk of low review scores (< 3) with an AUC of 0.67 using delivery delay, customer location, and related features. High-risk product categories (e.g., furniture and bulky items) exhibit roughly 2× higher late delivery rates, presenting clear opportunities for targeted logistics improvements.

## B. Project Links

- **Notebook**: [Google Colab Notebook](https://colab.research.google.com/drive/17L69MINJDPQG95oHFxiqyJM2BTvxvIg4?usp=sharing)  
  

- **Dashboard**: [https://your-streamlit-or-tableau-public-link](https://your-streamlit-or-tableau-public-link)

- **Presentation**: [https://docs.google.com/presentation/d/YOUR_SLIDES](https://docs.google.com/presentation/d/YOUR_SLIDES)  


## C. Technical Explanation

- **Data Cleaning**  
  Dates were converted to datetime with `errors='coerce'` to safely handle invalid values. Missing `review_score` values were imputed using the median (3.0). Non-delivered orders (statuses: canceled, unavailable, invoiced, processing, shipped without delivery date) were flagged as 'Not Delivered' and excluded from percentage-late calculations. Joins were performed carefully (`how='left'` or `how='inner'`) to prevent unintended row duplication.

- **Candidate's Choice Addition**  
  Implemented a PyTorch neural network to predict churn risk (defined as review_score < 3). Features include delivery delay (`Days_Difference`), customer state, month, and product category. The model achieves ~0.67 AUC on the test set.  
  **Business value**: This enables proactive identification of high-risk orders — allowing Veridi Logistics to intervene early (e.g., follow-up messages, goodwill gestures, expedited support, or logistics escalation) to potentially reduce negative reviews by 10–20%, improve customer satisfaction, and increase retention in a competitive e-commerce environment.
