# EDA guidelines

Good exploratory data analysis should be just that - exploratory. When you encounter a new dataset, the first goal is to get familiar with it and understand it the best you can. There will be lots of tinkering and failed experiments. Remember, data science is a science! This means making observations, generating hypotheses and then conducting experiments to test the hypotheses. It's an iterative process, but the goal is always to build the best model we can. EDA helps us do two things toward this goal:

1. Identify and fix problems in the data.
2. Utilize the data effectively to build the best model possible.

EDA is never exactly the same twice - the structure and quirks of each dataset will be different and therefore the best way to handle each dataset will be different. But, we can identify some common questions to ask and techniques to find answers as we clean up a data set and get it into place for model training.

Treat a new dataset like a new specimen - imagine you are an archeologist who just found a new fossil or an explorer who just arrived at an unexplored island. You want to understand and catalog as much information about your discovery as possible to tell a coherent story and draw strong conclusions.

## 1. Get to know your data

These are some initial, general questions that apply to practically any data set or data science problem. Finding these answers will get you oriented and start you off making effective and interesting observations.

- What are we trying to do with this data (e.g. is this a supervised or unsupervised problem? Is the goal regression, or classification, or something else?)
- How much data do we have?
  - How many features (columns) are there?
  - How many examples (rows) are there?
  - How big will the training and testing sets be after the split?
  - How big will the cross validation folds be?
- What data type is each feature (e.g. float, int, string, object, etc.)?
- What type of variable is each feature (e.g. continuous random variable, discrete random variable, nominal, ordinal, etc.)?
- For supervised machine learning tasks - what data and variable type are the labels?

There are many others - but these will get you started. Also, be prepared to go on side-quests. If you notice anything strange or interesting while answering these questions - pursue it! (Or make a note to pursue it later).

## 2. Clean up your data

Real data is often messy. It might contain errors or omissions. Don't ever trust data you have not inspected and don't assume anything. Once you have understood the general structure of the dataset, it's time to dig in see what we can do to clean it up. You may find some of these issues, all of them or none of them, and handling them correctly will depend on exactly how they manifest.

### 2.1. Things to look for

1. Check and set data-types. Pandas is usually smart enough to get this right, but take a look for yourself - sometimes there are problems. Example: numbers encoded as strings.
2. Look for features that obviously aren't useful data. Examples could be unique ID or row numbers, or columns with constant values.
3. Look for missing data. Sometimes this will come in the form of np.nan or pd.NA - but you will often find missing data hiding in the form of placeholder values. For example: '0' blood pressure in the diabetes dataset.
4. String data that needs to be encoded to numbers.
5. Look for extreme, incorrect or obviously nonsensical values. Example: '999' for pdays in the banking marketing data.
6. Look for low entropy features. Example: in the banking marketing data, there were only 2 defaults out of more than 25000 rows.
7. Look for highly correlated, anti-correlated or co-linear features.

### 2.2. Tools to use

#### 2.2.1. Observing data composition

- Pandas has several dataframe class methods to display data. Try on any dataframe: *.head(), .info(), .describe()*
- Graphical methods are your friend. Distribution plots can be a great way to spot many of the problems mentioned above. Pandas dataframes have a *.hist()* class method that allows you to easily plot a histogram for each column in a dataframe. Seaborn's boxplot can be a good option as well.

#### 2.2.2. Observing relationships in data

- Plotting features against each other is a great way to look for correlated numerical features. Favorite tools here are pyplot's *matshow()*, or Seaborn's *heatmap()* paired with Panda's *.corr()*.
- For investigating the relationship between individual features and the labels, the approach is going to depend a lot on what those features and labels are. For classification, you could split the features by their label and make boxplots. For regression, you could use a scatter plot.

### 2.3. What to do when you find problems

Any time you alter the dataset, you should make the change very clear and describe your justification. As a data scientist, your source of truth is data and therefore any time you are manipulating you data you need to be transparent and document what you are doing. Many of the techniques below can artificially improve model performance if misused.

#### 2.3.1. Missing data

Missing data can be a thorny problem. If the data is not there, we often have no way to get it back. Also, realize that they very fact that the data is missing may mean something. There are a few options on how to handle it:

1. Get rid of features which have large amounts of missing data. This can be risky as it causes us to lose even more data and may adversely affect model performance.
2. Get rid of observations which have missing data. The caution given for #1 applies here too.
3. Fill in missing data with a sane value. The value to choose will depend on the dataset, but we can often do better than zero.
4. Impute the value. Rather than using the feature mean or median to fill in the data, more advanced strategies use the other features to estimate what a missing value should have been.

#### 2.3.2. Extreme values

I hate the term 'outlier' - it leads to an overly simplistic view where every observation above or below some threshold is somehow 'bad' and needs to be discarded. It's easy to artificially inflate apparent model performance by trimming data and thus reducing its variability. Don't do this - it's essentially cheating. To think about extreme values correctly, realize that they are not all the same. They can show up for a few different reasons:

1. Place-holders for missing data.
2. Errors in data collection, measurement errors, equipment malfunctions. Ex: a damaged temperature sensor reports 999.

These are both essentially missing data. If the error can't be corrected, see the advice above for handling missing data.

3. Issues with data collection design or sampling. Observation that don't belong in the dataset often give extreme values. Example: if a professional ultra-marathon runner was included in the diabetes dataset.

A good dataset is designed to look at some aspect of a sample of a population. Therefore, all members of that sample should be members of the population. If the goal of the diabetes data was to predict diabetes in normal people, a highly conditioned elite athlete probably does not belong in the sample. If you can identify points like these, their removal is justified.

4. Natural variation in the population. This is the most common. But - don't remove these, unless you have a good, clear reason!

Many people use a threshold based on the interquartile range to remove or clip extreme values. This is a bad practice. When dealing with large datasets, you should expect to see some very large or very small values. For example, in a normally distributed population, we expect 99.7% of observations to fall within three standard deviations of the mean. But consider a dateset with 10,000 observations - you should expect about 30 observations to exceed the 'three-sigma' cut-off. The same logic applies to interquartile range based cutoffs. Applying them essentially throws away some fraction of data for no reason. Doing so may improve the model's apparent performance, but it does so by underestimating the true level of variation in the data, leading to a model that does not reflect reality and will not generalize well.

If you do decide to clip or remove outliers, you should document the examples you have removed and provide a justification. This is one time when 'it made the model more accurate' is not a good answer. Cherry-picking data is not a valid optimization strategy. If you can't explain why you think or how you know something is weird or wrong with a data point, you shouldn't exclude it.

**Example**: you are looking at a large sample of height measurements for people in the US. If you told me you excluded an example where someone was measured at 50 feet tall, I'd say, 'OK, sounds good'. If you said you were excluding everyone over 7 feet tall, I'd be skeptical and want you to justify why that's a valid cut-off in terms of the question you are trying to answer.

If you would like to dig into the complexity of outlier detection, take a look at '[There and back again: Outlier detection between statistical reasoning and data mining algorithms](https://findresearcher.sdu.dk:8443/ws/files/153197807/There_and_Back_Again.pdf) by Arthur Zimek and Peter Filzmoser at the University of Southern Denmark.

#### 2.3.3. Correlated features

Highly correlated features are often redundant and increase model size and/or compute time without helping performance. Luckily it's a little easier to justify removing correlated features than extreme values. Removing an entire feature is not cherry-picking observations, it excludes the same data from all observations. Three common techniques to reduce the number of features and only pick the 'best' features are:

1. Manual feature selection. Look at the data: the feature in question's correlation to other features and the labels. Decide to remove or not based on your observations.
2. Automatic feature selection: Scikit-learn includes several methods, search for 'feature selection' in the documentation.
3. Dimensionality reduction using techniques like principal component analysis. I again refer you to the Scikit-learn documentation on 'dimensionality reduction'.

However, you may not need to do anything at all about correlated features. One of the most powerful aspects of machine learning models is their ability to pick up on subtle variation and trends in and higher order interactions between features. Don't throw away features just because they look correlated.

Consider the following two examples. If your dataset contains the same temperature measurement in Celsius and Fahrenheit units, those features will be highly correlated - you obviously don't need both. But, if you are designing a model that predicts clothing size, arm span and height are probably highly correlated, but you likely want both in your dataset.

## 3. Improve your data

Once any junk has been removed and the data is 'clean' and formatted well enough to use in training, there are often still ways it can be improved. These approaches span EDA and feature engineering, but that is a common overlap. Remember, the goal of exploring the data is to determine how best to use it in model training. Here are some common approaches to 'polish' a dataset before training.

1. Scale it. The requirements here are model dependent, so read up on the model you are using. A quick google of 'how to scale data for model type x' should return lots of information.
2. Transform it. Some models can benefit from data that approximates specific distribution, in these cases operations like taking the log, or the Box-Cox transformation can be helpful.
3. Bin, smooth or otherwise normalize.
4. Anything else you can come up with!

They sky is really the limit here - the more creative and clever you are the better.
