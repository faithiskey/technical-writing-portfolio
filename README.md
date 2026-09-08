Building a Fraud Detection API with Machine Learning and FastAPI

Machine-learning models are useful only when they can be integrated into applications that people can actually use.

For one of my projects, I built a fraud-detection application that combines machine learning with FastAPI and Streamlit. The goal was to move beyond simply training a model in a notebook and create an application capable of accepting transaction data and returning a prediction.

From Data to Model

The workflow started with preparing the financial transaction dataset.

The major steps included:

- Loading and inspecting the dataset
- Handling missing values
- Exploring the distribution of the variables
- Preparing categorical and numerical features
- Splitting the data into training and testing sets
- Scaling features where necessary
- Training a classification model
- Evaluating model performance

One important lesson from the process was that model development is only one part of a machine-learning project.

Data quality and preprocessing have a major impact on the final result.

Why FastAPI?

After training the model, I wanted to make it accessible outside a Jupyter Notebook.

FastAPI provides a lightweight way to expose a machine-learning model through an API.

Instead of manually running Python code every time a prediction is required, a client application can send transaction information to an endpoint.

The basic flow becomes:

Transaction data → API → Preprocessing → ML model → Prediction

For example, a request can contain the relevant transaction features, and the API returns a prediction indicating whether the transaction is likely to be fraudulent.

Connecting the Model to an Application

I used Streamlit as the user-facing layer.

This created a simple architecture:

Streamlit UI → FastAPI → Machine-learning model

The separation is useful because the API handles the prediction logic while Streamlit handles the user interface.

It also makes the model easier to integrate with other applications in the future.

What I Learned

One of the biggest lessons from this project was that deploying a model is different from training one.

A model can perform well inside a notebook but still require additional work before it becomes part of a usable application.

Some of the important considerations include:

- Consistent feature preprocessing
- Matching training and prediction features
- Model serialization
- API validation
- Error handling
- Input formatting
- Reproducibility

I also encountered issues related to mismatched features between the trained model and prediction input. That experience reinforced how important it is to keep the preprocessing pipeline consistent between training and deployment.

Final Thoughts

Machine learning becomes much more useful when it moves beyond experimentation and into an application.

This project gave me practical experience connecting data preprocessing, machine learning, APIs, and a user interface into one workflow.

For me, the key takeaway is simple:

Building the model is only the beginning. Making it usable is where the engineering becomes important.














Why EDA and Data Cleaning Matter More Than the Model

When people talk about data science, machine-learning models often receive most of the attention.

XGBoost. Random Forest. Neural networks. Deep learning.

But before choosing a model, there is a more fundamental question:

Do we actually understand the data?

That is where Exploratory Data Analysis (EDA) and data cleaning become critical.

Start With the Data

Before building a model, I usually want to answer questions such as:

- What does each variable represent?
- Are there missing values?
- Are there duplicates?
- Are there unusual values?
- How are the variables distributed?
- Which variables appear related?
- Are there potential data-quality problems?

These questions can reveal problems that a machine-learning algorithm cannot magically fix.

Cleaning Is Not Just Removing Missing Values

Data cleaning is much broader than filling null values.

Depending on the dataset, it can involve:

- Handling missing observations
- Removing duplicates
- Correcting data types
- Identifying outliers
- Standardizing inconsistent values
- Checking impossible values
- Handling categorical variables
- Removing irrelevant columns

For example, a numerical column stored as text can cause problems later during analysis or modelling.

A simple inspection at the beginning can prevent unnecessary debugging later.

EDA Helps Connect Data to Business Questions

EDA isn't just about producing charts.

The goal is to understand what is happening in the dataset.

For example:

What happened?

Revenue increased or decreased.

When did it happen?

Certain periods may show stronger performance.

Why might it have happened?

A particular product category, customer group, location, or operational factor may explain the change.

What should we investigate next?

This is where data analysis becomes useful to decision-makers.

Visualization Is a Tool, Not the Final Answer

I use visualizations to make patterns easier to identify.

Depending on the problem, this could include:

- Distribution plots
- Bar charts
- Time-series plots
- Correlation analysis
- Box plots
- Category comparisons

But the chart itself isn't the insight.

The insight comes from interpreting what the chart means.

A good analyst should be able to move from:

Chart → Observation → Explanation → Business implication

Why This Matters for Machine Learning

Poor data preparation can affect model performance significantly.

If important variables are incorrectly formatted, missing, duplicated, or inconsistently processed, the model is learning from problematic inputs.

This is why I prefer to think about machine learning as a complete workflow:

Understand → Clean → Explore → Engineer → Model → Evaluate → Communicate

Not:

Load data → Train model → Done

My Main Takeaway

One of the biggest lessons I've learned while working on data-science projects is that a sophisticated model cannot compensate for poorly understood data.

Sometimes, better cleaning and better analysis can produce more value than simply switching to a more complex algorithm.

The model matters.

But understanding the data comes first.









From Jupyter Notebook to API: Deploying a Machine Learning Model

A machine-learning project often begins in a notebook.

You load the dataset, clean it, train a model, evaluate it, and save the results.

But what happens when someone else needs to use that model?

That was the motivation behind one of my deployment projects using FastAPI and Streamlit.

The Problem With Notebook-Only Models

A notebook is excellent for experimentation.

However, a business application usually needs something different.

Users shouldn't have to open a Jupyter Notebook and execute Python cells to get a prediction.

Instead, the model needs an interface.

One option is to expose the model through an API.

Introducing FastAPI

FastAPI makes it possible to create endpoints that accept input and return predictions.

The architecture can be represented as:

Client → FastAPI endpoint → preprocessing → model → prediction

The API receives structured input, validates it, prepares it in the same way as the training data, and sends it through the trained model.

The prediction is then returned to the client.

Adding Streamlit

For the user interface, I used Streamlit.

This provides a simple way to create an interactive application without building a complete frontend from scratch.

The user can enter the relevant information, submit it, and receive the model's prediction.

The overall system becomes:

User → Streamlit → FastAPI → ML model → Prediction → Streamlit

This separation also makes the project easier to reason about.

One of the Most Important Deployment Lessons

A model doesn't exist in isolation.

Suppose a model was trained using 39 features.

If the prediction application sends only 38 features, the model cannot correctly process the input.

This sounds obvious, but feature mismatches are common when moving from experimentation to deployment.

The solution is to maintain consistency between:

Training preprocessing

and

Prediction preprocessing

The same transformations, feature ordering, and expected inputs need to be maintained.

Model Serialization

Once the model is trained, it needs to be saved so the application can load it later.

Tools such as joblib can be used to serialize many Python machine-learning models and preprocessing objects.

However, version compatibility also matters.

A model saved using one version of a machine-learning library may produce warnings or compatibility issues when loaded using another version.

That is why documenting the environment is an important part of deployment.

What This Project Taught Me

The biggest lesson was that data science doesn't stop when the model reaches a good evaluation score.

A production-oriented workflow also needs to consider:

- Model persistence
- API design
- Input validation
- Preprocessing consistency
- Error handling
- Dependency versions
- User experience

The journey becomes:

Data → Analysis → Model → API → Application

And that final step is what makes the model accessible to actual users.

Final Thoughts

Building machine-learning models is important, but understanding how to connect those models to applications is equally valuable.

Working with FastAPI and Streamlit helped me understand the bridge between data science and software engineering.

It also changed how I think about ML projects.

A successful project isn't just:

“I trained a model.”

It is:

“I built something that someone can actually use.”
