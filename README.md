## Unlocking Employee Benefits: NLP-Powered Insights from Job Descriptions

### 📌 Project Overview
- I showcase how to create an **end-to-end machine learning pipeline** to extract and categorise **employee benefits in a structured format** from unstructured job descriptions at scale.
- This enables **benefit insight generation** that would be useful for business HR functions, or individuals who are curious what type of benefits should be expected at their level! (fix)

To achieve this, I trained **two ML models**:
- **Named Entity Recognition (NER) Model** -> Extracts benefits from job descriptions along with contextual details e.g. "We offer health, dental and pet insurance"
- **Text Classification Model** -> Categorises extracted benefits into a list of predefined benefit categories

**Example Output:**

<table>
    <thead>
        <tr>
            <th>Job Description</th>
            <th>Extracted Benefit</th>
            <th>Categorised Benefit</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3">"We at ABC ltd are looking to hire an Insights Analyst, offering benefits such as a pension plan matching up to 5% of employer contribution, cycle2work scheme, health insurance, and much more!"</td>
            <td>pension plan matching up to 5% of employer contribution</td>
            <td>Retirement_benefits</td>
        </tr>
        <tr>
            <td>cycle2work scheme</td>
            <td>Transport_benefits</td>
        </tr>
        <tr>
            <td>risk insurance</td>
            <td>Insurance_benefits</td>
        </tr>
    </tbody>
</table>
<br>

### 🎯 KPIs (Key Performance Indicators)
✅ **Extraction Accuracy** - Ensure benefits are extracted with full context (e.g., pension contribution %)  
✅ **Global Applicability** - Model is trained on job descriptions across **UK, US, Germany, India, Australia, France, and Canada**  
✅ **High Recall Rate** – Minimize overlooked benefits in job descriptions  
✅ **False Positive Minimization** – Avoid irrelevant extractions (e.g., distinguishing "health insurance" as a benefit vs. a job responsibility)  
<br>

### 📘 Project notebooks
- 📄 **[Using models to extract + classify benefits from job descriptions](/notebooks/Using_NER_and_Classificcation_models.ipynb)**
- 📄 **[Training NER model using spaCy](/notebooks/)**
- 📄 **[Training Text Classification model using spaCy](/notebooks/)**
- 📄 **[Extracting data using SQL](/notebooks/SQL_to_extract_data.ipynb)**

### 📂 Dataset
**Source:** Job descriptions **scraped from online job boards** and stored in **Databricks Catalog**  
- **Raw Data Format:** HTML  
- **Preprocessing:** Converted to plain text, tokenized for NLP model training  
- **Annotations:** Manually labeled via **Prodi.gy**, with:  
  - **2,000+ annotated JDs for NER**  
  - **3,500+ annotated JDs for Text Classification**  
<br>

### 🔑 Key steps
**1️⃣ Data Collection & Cleaning**  
- Extracted job descriptions from **Databricks data lake using SQL**  
- Cleaned text: removed HTML tags, tokenized sentences, lowercased words  

**2️⃣ Annotation & Model Training**  
- Created ground-truth, labeled dataset by annotating job descriptions manually using **Prodi.gy**
- Used a fine-tuned **BERT-based transformer models** for both NER & Classification

**3️⃣ Model Architecture**  
- **NER Model:** Uses **pre-trained BERT embeddings** + a custom NER component to detect **benefit phrases**  
- **Text Classification Model:** **Multi-label classifier** that assigns benefits to **one or more categories** based on model confidence  

**4️⃣ Model Evaluation & Iteration**  
- Performance measured via **Precision, Recall, and F1 Score** 
- Logged model perforance on **ML Flow and Weightsandbiases** for documentation and ease of future usage 
- Iterative **retraining & tuning** until models met business accuracy thresholds 
<br>

### 🚀 Challenges & Insights 
⚠️ **Handling Class Imbalance**  
Some benefit categories were **underrepresented in the training data**. 
**Solution:**  
- **Used data augmentation techniques** to artificially balance the dataset.  
- **Optimized loss functions** to prevent bias towards overrepresented classes.  

⚠️ **Extracting Benefits with Context**  
Job descriptions often **mention benefits vaguely** (e.g., “Great employee perks”).  
**Solution:** Custom rules to **ignore vague references** while preserving **relevant details** (e.g., pension contribution %).  

⚠️ **Avoiding False Positives**  
"Health Insurance Consultant" (job role) vs. "Health Insurance Provided" (benefit).  
**Solution:** Context-aware modeling using **Transformer-based embeddings** + custom **negative sampling during training**. 
