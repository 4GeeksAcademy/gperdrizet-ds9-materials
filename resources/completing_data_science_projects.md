# How to complete data science projects for submission

The projects in the next portion of the course each ask you to use a specific type of model to make predictions based on a dataset. These projects follow approximately the same format and steps, mirroring the workflow of a data scientist. The only real difference between them are the model type and the dataset (though a few even share the same dataset). The projects I am referring to are as follows:

1. [Logistic Regression](https://4geeks.com/syllabus/data-science-7/project/logistic-regression-project-tutorial)
2. [Linear Regression](https://4geeks.com/syllabus/data-science-7/project/linear-regression-project-tutorial)
3. [Regularized Linear Regression](https://4geeks.com/syllabus/data-science-7/project/regularized-linear-regression-project-tutorial)
4. [Decision Trees](https://4geeks.com/syllabus/data-science-7/project/decision-tree-project-tutorial)
5. [Random Forests](https://4geeks.com/syllabus/data-science-7/project/random-forest-project-tutorial)
6. [Boosting Algorithms](https://4geeks.com/syllabus/data-science-7/project/boosting-algorithms-project-tutorial)
7. [Naive Bayes](https://4geeks.com/syllabus/data-science-7/project/naive-bayes-project-tutorial)
8. [K-nearest Neighbors](https://4geeks.com/syllabus/data-science-7/project/k-nearest-neighbors-project-tutorial)

The instructions in the 4Geeks README for each project are approximately:

- **Step 1**: Load the dataset
- **Step 2**: Perform a full EDA
- **Step 3**: Build a model
- **Step 4**: Optimize the model

For these projects, I will provide you with a (mostly) blank 'MVP' (or minimum viable product) notebook based on those instructions to use as a starting point.

There will be variations and tools and techniques specific to each individual project, but they are essentially the same. This is good for us - it means if we can finish one of these projects, the others will be much easier. Let's expand on these instructions and generalize them so that you know what to include in your project submission.

## 1. Data loading

1. Load the data into a Pandas dataframe.
2. Look at the features and label names, types and overall amounts of data.
3. Split the data into training and testing features and labels.
4. Encode string features if necessary.

## 2. EDA

### 2.1. Baseline model performance

If possible, set/estimate/determine baseline model performance. It is useful to do this early because it will give us a standard of comparison to judge how effective everything else we do actually is. This may not be possible, or it may be trivial, depends on the model and data.

### 2.2. Data composition & cleaning

1. Show the summary descriptive statistics for each feature.
2. Show the feature distributions using an appropriate plot.
3. Based on the information gained from 1 and 2, note and discuss extreme values or missing data if present.
4. Implement a strategy to deal with missing or extreme values if any.
5. Apply any other data cleaning indicated by your observations of the data.

### 2.3. Feature interactions & selection

1. Plot and/or quantify the interactions between sets of features using an appropriate method based on the statistical data type.
2. Plot and/or quantify the interaction between each feature and the target.
3. Based on your observations in 1 and 2, discuss any pathologies or irrelevant features.
4. Use the results of your analysis and/or automated methods to select features to use in your model.

## 3. Model training

1. Train the model with defaults on the training data.
2. Evaluate the model's performance.

## 4. Model optimization

1. Make improvements to the model or data.
2. Re-train the model.
3. Evaluate the new model's performance.
4. Repeat.

## Other tips for good, professional looking notebooks

1. Commit often! Every step in the above instructions should be at least one commit. Also, write good, short commit messages: 'Implemented SciKit-Learn StandardScaler for feature transformations.', 'Completed first hyperparameter tuning experiment.' etc.
2. Comment your code - use the '#' symbol to add comments to code blocks. Comments should be short and succinct, telling the reader what each call does.
3. Add explanations using Markdown text. As you move through the project, explain what you are doing at each step and why as well as any observations and conclusions.
4. Take advantage of the outline using Markdown formatting. Jupyter will extract an outline from a notebook that has headings defined. You can then display the outline in the activities panel. This is a great tool to stay organized and guide your reader.
5. Make sure you save and commit a final clean run before pushing notebooks to GitHub. Remember, once it's on GitHub, it's public. Unfinished work is fine, but errors or garbage or half run/run out of order notebooks look bad.
