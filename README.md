# Machine-Learning-Challenge
# The Logistics Auditor

## A. Executive Summary

Veridi Logistics (Olist) experiences late deliveries in approximately 8–12% of orders overall, with Northeastern and Northern states showing significantly higher rates (e.g., AL 20.8%, MA 17.1%, SE 15.0%) compared to SP (~3–5%). Late and especially Super Late deliveries strongly correlate with poor customer reviews (average scores of 3.0 and 1.7 respectively, versus 4.3 for On Time), confirming that inaccurate estimated delivery dates are a major driver of negative sentiment and potential customer churn. A prototype LLM-powered recommendation engine was developed to suggest faster, more reliable alternative product categories for customers in high-risk regions or categories (e.g., avoiding furniture/bulky items in Northeastern states), offering a practical way to maintain trust and reduce disappointment even when delays occur. High-late categories (e.g., furniture and bulky items) exhibit roughly 2× higher delay rates, highlighting clear opportunities for targeted carrier adjustments and ETA refinements.

## B. Project Links

- **Notebook**: [Google Colab Notebook](https://colab.research.google.com/drive/17L69MINJDPQG95oHFxiqyJM2BTvxvIg4?usp=sharing)  
  

- **Dashboard**: [Dashboard](https://your-streamlit-or-tableau-public-link)

- **Presentation**: [Presentation Slides](https://www.canva.com/design/DAHBe0Jys5k/mDTndpBLV6Op-pV5X5RsDA/edit?utm_content=DAHBe0Jys5k&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)  


## C. Technical Explanation

- **Data Cleaning**  
  Dates were converted to datetime with `errors='coerce'` to safely handle invalid values. Missing `review_score` values were imputed using the median (3.0). Non-delivered orders (statuses: canceled, unavailable, invoiced, processing, shipped without delivery date) were flagged as 'Not Delivered' and excluded from percentage-late calculations. Joins were performed carefully (`how='left'` or `how='inner'`) to prevent unintended row duplication.

- **Candidate's Choice Addition**  
 Built a prototype LLM-powered product recommendation engine (using free-tier API).
The system takes customer state, purchased category, and delivery risk as input, then suggests 3 alternative categories that are more reliable/faster in that region and have higher historical satisfaction.
Business value: In high-late-risk areas or categories, proactive alternative suggestions can maintain customer trust, reduce disappointment from delays, increase conversion on related items, and indirectly lower churn even when logistics issues occur. This turns a pain point into an upsell/cross-sell opportunity.

## Tech Stack

- **Data Processing & Analysis**: Python 3.12, Pandas (for joins, aggregations, cleaning), Plotly Express (for interactive charts)
- **Machine Learning / LLM**: Groq API + OpenAI client library (for Llama 3.1 model inference)
- **Dashboard**: Gradio (for interactive web app with filters, plots, and LLM recommendations)
- **Environment**: Google Colab (for development and sharing)
- **Dataset**: Olist Brazilian E-Commerce Public Dataset (from Kaggle) – raw CSVs processed into master dataset

## Instructions / Files Used

This project uses the Olist dataset split across multiple CSVs. All raw data is processed in the notebook to create a unified "master" dataset for analysis and dashboarding.

### Key Files:
- **Raw CSVs** (not uploaded to repo – too large; download from Kaggle: [Olist Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)):
  - `olist_orders_dataset.csv`: Core orders with timestamps, status, estimated/actual delivery dates.
  - `olist_order_reviews_dataset.csv`: Review scores and creation dates.
  - `olist_customers_dataset.csv`: Customer locations (state, city).
  - `olist_order_items_dataset.csv` & `olist_products_dataset.csv`: Product details and categories.
  - `product_category_name_translation.csv`: Portuguese-to-English category mapping (for bonus story).

- **Processed CSV** (uploaded to repo):
  - `master_logistics_audit.csv`: Unified dataset (~99k rows) after joins, cleaning, and feature engineering (e.g., `Days_Difference`, `Delivery_Status`, translated categories). Used as input for dashboard and analysis.

- **Notebook Files** (uploaded to repo):
  - `data_analysis_notebook.ipynb`: Main Jupyter notebook with data loading, cleaning, joins, delay calculations, geographic/sentiment analysis, and LLM prototype code. Includes all charts and outputs.
  - `app.py`: Gradio app script for the interactive dashboard (run with `gradio app.py` or in Colab). Features state filters, plots, and live LLM recommendations.

### How to Run Locally / Reproduce:
1. Download raw CSVs from Kaggle and place in a folder (e.g., `/data/`).
2. Open `data_analysis_notebook.ipynb` in Jupyter/Colab → run all cells to generate `master_logistics_audit.csv`.
3. Run the dashboard: `pip install gradio openai plotly pandas` → `python app.py` (or in Colab: paste and run the Gradio cell).
4. For LLM: Add your free Groq API key (console.g
