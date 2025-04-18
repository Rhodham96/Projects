class: impact

# Building an Automated EDA Agent with Gemini
## Transforming Kaggle Competition Workflows

.center[![EDAgent Illustration](https://miro.medium.com/v2/resize:fit:1400/1*-dpU7x5zEdFtCZYXnVjzGw.jpeg)]

???

Welcome! In this presentation, we're diving into how I used Google’s Gemini model to build an autonomous agent that automates exploratory data analysis for Kaggle competitions. Let’s explore how it works.

---

# Introduction

Data scientists often spend hours on exploratory data analysis (EDA) when starting a new Kaggle competition. What if we could automate this process using generative AI? In this presentation, I’ll share how I built an intelligent EDA Agent powered by Google’s Gemini model that can:

- Download competition data
- Generate comprehensive analyses
- Create both static and interactive visualizations
- Provide meaningful insights

All with minimal human intervention.

???

Exploratory Data Analysis, or EDA, is a critical step in any data science project. However, it’s also one of the most time-consuming. My goal was to automate this process using generative AI, specifically Google’s Gemini model, to save time and maintain high-quality analysis.

---

# The Problem: EDA is Time-Consuming but Critical

Every data scientist knows the drill:

- Download the competition data
- Check for missing values
- Plot distributions
- Look for correlations
- Understand the dataset before building models

This process typically takes hours and involves writing similar code for each new competition.

**Challenges:**

- Understand the context of any Kaggle competition
- Download and analyze the relevant datasets
- Generate appropriate visualizations
- Provide meaningful insights to guide modeling decisions

???

The problem is clear: EDA is essential but repetitive and time-consuming. For every new Kaggle competition, we go through the same steps, writing similar code each time. The challenge was to create a system that could handle all these tasks autonomously.

---

# The Solution: An Intelligent EDA Agent

My solution combines the Kaggle API with Google’s Gemini model to create an end-to-end EDA agent.

```python
eda_agent = EDAAgent(api_key)
result = eda_agent.analyze_competition("spaceship-titanic")
```

With just these few lines of code, the agent:

- Downloads all competition data
- Identifies the training dataset
- Generates a comprehensive EDA report with visualizations
- Provides competition context and insights

???

The solution is an intelligent EDA Agent that combines the Kaggle API with Google’s Gemini model. With just a few lines of code, the agent handles everything from downloading data to generating insights.

---

# System Architecture

The system consists of two main components:

1. **KaggleDownloader**: Handles authentication and downloading of competition data
2. **EDAAgent**: Core component that generates and executes EDA code

**KaggleDownloader Class:**

```python
class KaggleDownloader:
    def __init__(self, check_credentials=True):
        self.temp_dir = tempfile.mkdtemp()
        self.api = KaggleApi()
        try:
            self.api.authenticate()
            self.authenticated = True
        except Exception as e:
            self.authenticated = False
            # Error handling...

    def download_competition(self, competition_name, target_dir=None):
        # Download competition data using Kaggle API
        # Extract zip files
        # Return path to data
```

**EDAAgent Class:**

```python
class EDAgent:
    def __init__(self, api_key):
        genai.configure(api_key=api_key)
        self.llm = genai.GenerativeModel('gemini-2.5-pro-exp-03-25')
        self.downloader = KaggleDownloader()
        self.use_interactive = True  # Enable interactive visualizations

    def analyze_competition(self, competition_input):
        # Download competition data
        # Get competition info from LLM
        # Generate and execute EDA code
        # Create comprehensive report with visualizations
```

???

The system architecture is divided into two main components: the KaggleDownloader, which handles data retrieval, and the EDAgent, which is the core of the system, generating and executing EDA code.

---

# Gen AI Capabilities in Action

1. **Structured Output/Controlled Generation**

The agent generates structured Python code for EDA. Here’s an example prompt:

```python
prompt = f"""
Generate Python code for a comprehensive exploratory data analysis of a dataset for the Kaggle competition.

Dataset information:
- Shape: {df.shape}
- Columns: {', '.join(df.columns)}
- Info: {df_info}
- First few rows: {df.head(3).to_string()}

Competition information:
- Title: {competition_info.get('title', 'Not available')}
- Description: {competition_info.get('description', 'Not available')}
- Evaluation metric: {competition_info.get('evaluation_metric', 'Not available')}
- Goal: {competition_info.get('goal', 'Not available')}

Create a DETAILED and COMPREHENSIVE EDA script that includes BOTH static (matplotlib/seaborn)
AND interactive (Plotly) visualizations:
...
"""
```

2. **Function Calling**

The agent generates executable Python code that performs specific data analysis functions:

```python
def execute_code(self, code_to_execute, local_vars=None):
    # Set up execution environment
    # Execute the LLM-generated code
    # Capture output and visualizations
    # Return results
```

3. **Agents**

The system acts as an autonomous agent:

```python
result = eda_agent.analyze_competition("spaceship-titanic")
```

???

The agent leverages advanced Gen AI capabilities like structured output generation, function calling, and autonomous workflow management. It generates Python code for EDA, executes it, and produces comprehensive reports.

---

# Example Output: Spaceship Titanic Competition

When analyzing the Spaceship Titanic competition, the agent:

- Downloaded the competition data
- Generated an introduction explaining the competition goal
- Created comprehensive EDA code with visualizations
- Identified key patterns in the data

**Snippets of the Generated Analysis:**

```
--- 1. Data Overview ---
Dataset Shape: (8693, 14)

Dataset Info:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 8693 entries, 0 to 8692
Data columns (total 14 columns):
 #   Column        Non-Null Count  Dtype    
---  ------        --------------  -----    
 0   PassengerId   8693 non-null   object   
 1   HomePlanet    8492 non-null   object   
 2   CryoSleep     8476 non-null   object   
 3   Cabin         8494 non-null   object   
 4   Destination   8511 non-null   object   
 5   Age           8514 non-null   float64  
 6   VIP           8490 non-null   object   
 7   RoomService   8512 non-null   float64  
 8   FoodCourt     8510 non-null   float64  
 9   ShoppingMall  8485 non-null   float64  
 10  Spa           8510 non-null   float64  
 11  VRDeck        8505 non-null   float64  
 12  Name          8493 non-null   object   
 13  Transported   8693 non-null   bool     
dtypes: bool(1), float64(6), object(7)  
memory usage: 891.5+ KB

--- 2. Missing Values Analysis ---
Missing Value Counts and Percentages:
 Count  Percentage  
CryoSleep       217    2.496261  
ShoppingMall    208    2.392730  
VIP             203    2.335212  
HomePlanet      201    2.312205  
Name            200    2.300702  
Cabin           199    2.289198  
VRDeck          188    2.162660  
FoodCourt       183    2.105142  
Spa             183    2.105142  
Destination     182    2.093639  
RoomService     181    2.082135  
Age             179    2.059128
```

**EDA Summary and Next Steps:**

```
Key Findings:
- Target Variable ('Transported') is relatively balanced (~50/50 split).
- Significant amount of missing data in multiple columns, especially
  'CryoSleep', 'ShoppingMall', 'VIP', 'Name', 'Cabin'. Missingness patterns
  exist (e.g., related spending columns).
- Feature Engineering: Extracted 'GroupId', 'MemberId', 'Cabin_Deck',
  'Cabin_Num', 'Cabin_Side'. Created 'TotalSpending' and 'IsSpending'.
- Strong Predictors Identified:
  - CryoSleep: Very strong positive correlation with being transported
  (CryoSleep=True -> High Transport rate). Passengers in CryoSleep have zero
  spending.
  - Spending: Higher spending (RoomService, Spa, VRDeck, TotalSpending)
  strongly correlates with NOT being transported.
  - Cabin Deck: Decks B, C, G have significantly higher transport rates.
  - HomePlanet: Europa passengers have higher transport rates, Earth lower.
  - Age: Younger passengers seem slightly more likely to be transported.
- Moderate/Weak Predictors:
  - Cabin Side: Side 'S' slightly higher transport rate.
  - Destination: '55 Cancri e' higher transport rate.
  - VIP: Non-VIPs slightly more likely to be transported (but VIPs are rare).
- Feature Distributions: Spending features are heavily skewed towards zero.
  Age distribution is multimodal.

Potential Next Steps:
1. **Missing Value Imputation:** Develop strategies based on findings
  (e.g., median/mean for Age, mode for categorical, potentially using
  relationships like CryoSleep=True -> Spending=0, or more advanced methods
  like KNNImputer). Consider imputing Cabin components separately.
2. **Feature Engineering Refinement:**
    - Create features related to group size from 'GroupId'.
    - Bin 'Age' into categories (Child, Teen, Adult, Senior).
    - Log transform skewed numeric features (like spending) for certain models.
    - Create interaction features (e.g., HomePlanet * CryoSleep).
    - Extract titles or family names from 'Name' (though 'Name' has many NaNs).
3. **Categorical Feature Encoding:** Apply appropriate encoding methods
  (One-Hot Encoding, Target Encoding) based on cardinality and model choice.
4. **Outlier Handling:** Investigate extreme values in spending features and
  decide on handling (clipping, transformation, removal - be cautious).
5. **Modeling:** Select and train classification models (Logistic Regression,
  Random Forest, Gradient Boosting - like LightGBM/XGBoost) and evaluate
  using the competition metric (if known, otherwise use standard metrics
  like Accuracy, F1-score).
6. **Cross-Validation:** Use robust cross-validation (e.g., StratifiedKFold)
  to get reliable performance estimates.

EDA Complete.
```

.center[![Visualization 1](https://miro.medium.com/v2/resize:fit:3424/1*EGDE1nEuJkD7QkvxIl1bug.png)]

.center[![Visualization 2](https://miro.medium.com/v2/resize:fit:2294/1*FknfOyxR7dTBUJNg50xIkQ.png)]

???

Here’s an example of the agent in action, analyzing the Spaceship Titanic competition. It provides a detailed overview, missing value analysis, and identifies key predictors. The agent also generates both static and interactive visualizations for deeper insights.

---

# Conclusion

This project demonstrates how generative AI can transform data science workflows by automating repetitive tasks while maintaining high quality. By combining Google’s Gemini model with the Kaggle API, we’ve created a system that can:

- Save significant time in the initial exploration phase
- Provide comprehensive analysis with both static and interactive visualizations
- Generate contextual insights that guide further analysis
- Adapt to different competition types and datasets

The code is available in my [Kaggle notebook](https://www.kaggle.com/code/robinhamers/edagent-genaicapstone-project/) (public after April 20th), and I welcome feedback and contributions.

.center[![Conclusion Image](https://miro.medium.com/v2/resize:fit:1400/0*Llxgv0b4VbKubO_K)]

???

In conclusion, this project shows the potential of generative AI to revolutionize data science workflows. By automating EDA, we save time and gain deeper insights. The code is available for further exploration, and I look forward to your feedback and contributions.

---

# Limitations and Future Work

**Current Limitations:**

- **Domain Knowledge**: The agent lacks specific domain expertise crucial for some competitions.
- **Model Selection**: It doesn’t recommend specific models based on data characteristics.
- **Feature Engineering**: Suggests but doesn’t implement feature engineering ideas.

**Future Enhancements:**

- Model recommendation based on data characteristics
- Automated feature importance analysis
- A more interactive UI

???

While the system is powerful, it has limitations like lacking domain-specific knowledge and not implementing feature engineering. Future work will focus on enhancing these areas, including model recommendations and a more interactive UI.

---

class: impact

# Thank You!

.center[![LinkedIn](https://miro.medium.com/v2/resize:fit:1400/0*Llxgv0b4VbKubO_K)]

**Connect with me:** [LinkedIn](https://www.linkedin.com/in/robin-hamers/)

???

Thank you for your attention! If you have any questions or want to connect, feel free to reach out on LinkedIn. Let’s continue the conversation!
