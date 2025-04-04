# Offensive Post Detection Pipeline

This repository implements a complete NLP pipeline to detect offensive language in social media posts. The approach combines robust text preprocessing, feature extraction, model training, and prediction generation. Below is a high-level summary of the workflow:

---

## 1. Environment Setup

- **Library Installation:**  
  Installs essential NLP packages including `contractions`, `pyspellchecker`, `emoji`, `imbalanced-learn`, and `wordcloud`.

- **Imports & Configuration:**  
  Loads core libraries (Pandas, NumPy, regex, logging) along with NLP tools from SpaCy and NLTK. It also sets up machine learning libraries (scikit-learn, XGBoost) and configures logging, downloads necessary NLTK resources, and suppresses warnings.

---

## 2. Data Loading & Inspection

- **Data Import:**  
  Reads the training data from a CSV file (`train.csv`).

- **Initial Quality Checks:**  
  Inspects the dataset’s shape and checks for missing values or empty strings in the text column ("tweet").

---

## 3. Text Preprocessing

- **Text Cleaning:**  
  A custom function removes HTML entities, URLs, mentions, hashtags, emojis (converting them to text), special characters, and repeated letters. The text is converted to lowercase and extra spaces are removed.

- **Tokenization & Negation Handling:**  
  Uses SpaCy to tokenize the cleaned text while tagging words following negation terms (e.g., "not good" becomes "not_good") to preserve sentiment context.

- **Lemmatization:**  
  Applies SpaCy’s lemmatizer to reduce words to their base forms, ensuring consistency.

- **Stopword Removal:**  
  Filters out common stopwords while retaining important nouns and verbs.

- **Saving Processed Data:**  
  The final preprocessed text is saved to a CSV file for future use.

---

## 4. Exploratory Data Analysis (EDA)

- **Label & Text Length Analysis:**  
  Visualizes class distribution (using count plots and pie charts) and analyzes the distribution of text lengths with histograms.

- **Word Frequency Analysis:**  
  Identifies the most common words and generates a word cloud to reveal dominant themes.

- **Missing Value Visualization:**  
  Uses heatmaps to confirm the completeness of the dataset.

---

## 5. Feature Extraction

- **Count Vectorization:**  
  Converts text into a numerical matrix based on word counts.

- **TF-IDF Transformation:**  
  Applies TF-IDF (with various configurations like unigrams, bigrams, and trigrams) to weigh the importance of words.

- **Word Embeddings:**  
  Uses pre-trained GloVe embeddings to generate dense, 100-dimensional representations of the text.

- **Dimensionality Reduction:**  
  Applies PCA and t-SNE to visualize high-dimensional feature spaces in 2D.

---

## 6. Handling Class Imbalance

- **SMOTE:**  
  Balances the dataset by generating synthetic samples for underrepresented classes, ensuring fair model training.

---

## 7. Model Training & Evaluation

- **Model Selection:**  
  Evaluates multiple classifiers such as SVM (with RBF kernel), Decision Tree, Naïve Bayes, Random Forest, XGBoost, and an ensemble Voting Classifier.

- **Dynamic Pipeline:**  
  A custom function applies a chosen TF-IDF vectorization method, encodes labels, uses SMOTE for balancing, splits the data, trains the model, and evaluates performance using accuracy metrics, classification reports, and confusion matrices.

- **Optimization:**  
  Various TF-IDF configurations (e.g., sublinear scaling, binary presence, L1/L2 normalization) are tested to determine the optimal setup.

---

## 8. Final Model Deployment & Prediction

- **Best Model Training:**  
  The top-performing model is retrained on the full preprocessed training data.

- **Test Data Processing:**  
  The test dataset is preprocessed using the same pipeline as the training data.

- **Prediction Generation:**  
  The final model generates predictions, which are saved to a CSV file with corresponding IDs for submission or further analysis.

---

## Conclusion

This pipeline demonstrates a thorough and modular approach to offensive language detection in social media posts. By combining advanced text preprocessing techniques with dynamic model selection and rigorous evaluation, the system achieves high accuracy and robustness, making it easily adaptable to similar NLP classification tasks.
