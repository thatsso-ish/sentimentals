Overview
This code performs sentiment analysis on a dataset using the Natural Language Toolkit (NLTK) library's Vader sentiment analyzer. The dataset is loaded from a CSV file ('Dataset-SA.csv'), and various preprocessing steps are applied to clean and prepare the text data for analysis. The sentiment analysis results are then stored in a new column named 'Sentiment.'

Libraries Used
pandas: Data manipulation and analysis library.
nltk: Natural Language Toolkit for natural language processing.
re: Regular expression operations for text cleaning.
string: String manipulation functions.
math: Mathematical functions.

Setup
Before running the code, make sure to install the necessary libraries:
pip install pandas nltk
Additionally, download NLTK's stopwords dataset by running:
import nltk
nltk.download('stopwords')

Loading and Exploring the Dataset
pddf = pd.read_csv('Dataset-SA.csv')
pddf.shape
pddf.describe()
pddf.info()

Cleaning and Preprocessing Text
A function named clean is defined to perform text cleaning:
def clean(text):
    # ... (various cleaning steps)
    return text
Apply the cleaning function to the 'Review' column:
pdDF["Review"] = pdDF["Review"].apply(clean)

Handling Missing Values
Remove rows with missing values in the dataset:
pdDF.isnull().sum()
pdDF.dropna(inplace=True)
pdDF = pdDF.drop_duplicates(keep=False)

Handling Numeric Columns
Convert 'product_price' and 'Rate' columns to numeric format and remove rows with missing values:
pdDF['product_price'] = pd.to_numeric(pdDF['product_price'], errors='coerce')
pdDF['Rate'] = pd.to_numeric(pdDF['Rate'], errors='coerce')
pdDF = pdDF.dropna(subset=['product_price', 'Rate'], how='all')

Text Capitalization
Capitalize the first letter of each word in text columns:
pdDF['Review'] = pdDF['Review'].apply(capitalize_if_string)
pdDF['Summary'] = pdDF['Summary'].apply(capitalize_if_string)
pdDF['Sentiment'] = pdDF['Sentiment'].apply(capitalize_if_string)

Rounding Numeric Columns
Round off decimal values in 'product_price' and 'Rate' columns:
pdDF['product_price'] = pdDF['product_price'].round(0)
pdDF['Rate'] = pdDF['Rate'].round(0)

Removing Stopwords
Define a function to remove stopwords and apply it to text columns:
def remove_stopwords(word_list):
    # ... (remove stopwords)
    return processed_word_list

pdDF['Stopwords_Review'] = pdDF['Review'].apply(lambda x: remove_stopwords(x.split()) if isinstance(x, str) else x)
pdDF['Stopwords_Summary'] = pdDF['Summary'].apply(lambda x: remove_stopwords(x.split()) if isinstance(x, str) else x)

Miscellaneous
pdDF['product_name'] = pdDF['product_name'].str.replace('?', '')
pdDF = pdDF.style.set_properties(**{'text-align': 'left'})
pdDF

Note: The final dataframe is formatted for left alignment for better readability.
