# Text Classification Web App

This project is a Flask-based web application designed for classifying text in both Bengali and English into predefined topics. It leverages machine learning models to predict topics such as Politics, Corruption, Mob Justice, and more, based on user-provided text or uploaded CSV files. The application supports text preprocessing, tokenization, and topic prediction, with a user-friendly interface for real-time interaction.

## Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Model Training](#model-training)
- [Contributing](#contributing)
- [License](#license)

## Features
- **Text Classification**: Predicts topics for single text inputs in Bengali or English.
- **Batch Processing**: Upload a CSV file with "Context" and "Training Topic" columns to classify multiple texts and download results.
- **Preprocessing**: Cleans and tokenizes text, handling both Bengali and English inputs using regex and IndicNLP tokenization.
- **Error Handling**: Provides user feedback for invalid inputs or file formats.
- **Downloadable Results**: Saves batch predictions as a CSV file for download.
- **Interactive UI**: Built with HTML templates for a seamless user experience.

## Technologies Used
- **Python**: Core programming language.
- **Flask**: Web framework for building the application.
- **Pandas**: Data manipulation and CSV processing.
- **Scikit-learn**: Machine learning model (Random Forest) and TF-IDF vectorization.
- **IndicNLP**: Tokenization for Bengali text.
- **Joblib**: Model persistence.
- **HTML/CSS**: Frontend for the web interface.
- **Jupyter Notebook**: Model training and experimentation.
- **Transformers**: Zero-shot classification for initial label prediction (BART model).

## Installation
To set up the project locally, follow these steps:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/shehab0911/Text_Classification.git
   cd your-repo-name
   ```

2. **Create a Virtual Environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   Ensure you have the following packages:
   - flask
   - pandas
   - scikit-learn
   - joblib
   - indic-nlp-library
   - transformers
   - numpy
   - regex

4. **Download Pretrained Models**:
   Place the pretrained model files (`model.pkl`, `vectorizer.pkl`, `label_encoder.pkl`) in the `save model/` directory. These files are generated from the training notebook (`model.ipynb`).

5. **Run the Application**:
   ```bash
   python app.py
   ```
   The app will be available at `http://127.0.0.1:5000`.

## Usage
1. **Single Text Prediction**:
   - Navigate to the homepage.
   - Enter text (Bengali or English) in the provided text box.
   - Submit to view the cleaned text and predicted topic.

2. **Batch Prediction**:
   - Upload a CSV file containing "Context" and "Training Topic" columns.
   - The app processes the file, filters valid topics, and displays a preview of the first 10 predictions.
   - Download the full results as `real_world_predictions.csv`.

3. **Error Handling**:
   - Empty text inputs or invalid CSV files trigger user-friendly error messages.
   - Only topics matching the pretrained label encoder are processed.

## Project Structure
```
your-repo-name/
├── app.py                   # Main Flask application
├── model.ipynb              # Jupyter notebook for model training
├── save model/              # Directory for pretrained models
│   ├── model.pkl
│   ├── vectorizer.pkl
│   ├── label_encoder.pkl
├── templates/               # HTML templates
│   ├── index.html
├── static/                  # Static files (CSS, JS)
├── requirements.txt         # Python dependencies
├── README.txt               # This documentation
```

## Model Training
The model training process is detailed in `model.ipynb`. Key steps include:

1. **Data Preprocessing**:
   - Load dataset from an Excel file (`Data & Topics (1).xlsx`).
   - Extract hashtags and map them to topics (e.g., `#corruption` → "Corruption").
   - Clean text by removing hashtags, URLs, mentions, and special characters.

2. **Label Prediction**:
   - Use zero-shot classification (BART model) to predict topics for texts without hashtag-based labels.
   - Validate predicted labels against a predefined topic list.

3. **Model Training**:
   - Use TF-IDF vectorization with bigrams and a maximum of 5000 features.
   - Train a Random Forest classifier on the preprocessed dataset.
   - Evaluate model performance using precision, recall, and a confusion matrix.

4. **Model Saving**:
   - Save the trained model, vectorizer, and label encoder using Joblib for use in the Flask app.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request with a clear description of your changes.

Please ensure your code follows PEP 8 guidelines and includes relevant tests.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
Happy classifying! 🚀 For any issues or suggestions, please open an issue on GitHub.
