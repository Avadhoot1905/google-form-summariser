# Google Form Response Summarizer

This project provides a modular solution for analyzing Google Form responses using HDBSCAN clustering to identify common themes and patterns in the feedback.

## 📂 Project Structure

The analysis is split into 4 focused notebooks that pass data between each other:

1. **`1_get_google_form_responses.ipynb`** - Fetch form data via Google API
2. **`2_preprocess_data.ipynb`** - Clean and vectorize text responses  
3. **`3_apply_clustering.ipynb`** - Apply HDBSCAN clustering
4. **`4_summarise_results.ipynb`** - Generate insights and final outputs

## Features

- 🔗 **Google Forms API Integration**: Direct connection to fetch form responses
- 🔍 **Text Preprocessing**: Advanced text cleaning and preprocessing  
- 🎯 **HDBSCAN Clustering**: Intelligent grouping of similar responses
- 📊 **Comprehensive Analysis**: Sentiment analysis, word clouds, and statistics
- 📈 **Rich Visualizations**: Interactive charts and plots
- 📝 **Automated Reports**: CSV exports and summary reports
- 🧩 **Modular Design**: Each step can be run independently

## Setup Instructions

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Google API Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the Google Forms API
4. Create credentials:
   - Go to "Credentials" → "Create Credentials" → "OAuth 2.0 Client ID"
   - Choose "Desktop application"
   - Download the JSON file and rename it to `credentials.json`
5. Place `credentials.json` in the project root directory

### 3. Get Your Form ID

1. Open your Google Form
2. Click "Send" → "Link" 
3. Copy the form ID from the URL: `https://docs.google.com/forms/d/{FORM_ID}/edit`

### 4. Run the Analysis

**Execute the notebooks in order:**

1. **Part 1**: Open `1_get_google_form_responses.ipynb`
   - Replace `YOUR_FORM_ID_HERE` with your actual form ID  
   - Run all cells to fetch and save form data
   - Creates: `raw_form_responses.pickle`, `form_metadata.json`

2. **Part 2**: Open `2_preprocess_data.ipynb`
   - Run all cells to clean and vectorize text
   - Creates: `preprocessed_data.pickle`

3. **Part 3**: Open `3_apply_clustering.ipynb` 
   - Run all cells to perform HDBSCAN clustering
   - Creates: `clustered_data.pickle`

4. **Part 4**: Open `4_summarise_results.ipynb`
   - Run all cells to generate final analysis and reports
   - Creates: `final_analysis_results.csv`, `cluster_summary_report.txt`

## Output Files

- **Intermediate files**: `.pickle` files for passing data between notebooks
- **Final outputs**:
  - `final_analysis_results.csv`: Complete results with cluster assignments  
  - `cluster_summary_report.txt`: Detailed analysis report with insights

## Key Parameters

### HDBSCAN Configuration
- `min_cluster_size`: Minimum number of responses to form a cluster
- `min_samples`: Minimum samples in a neighborhood for core points

### TF-IDF Configuration
- `max_features`: Maximum number of features to extract
- `min_df`: Ignore terms appearing in less than min_df documents
- `max_df`: Ignore terms appearing in more than max_df fraction of documents

## Example Use Cases

- **Survey Analysis**: Group similar feedback themes
- **Customer Support**: Identify common issues and complaints
- **Event Feedback**: Understand attendee experiences
- **Product Reviews**: Categorize user opinions
- **Educational Surveys**: Analyze student feedback patterns

## Understanding the Results

### Clusters
Each cluster represents a group of responses with similar content. The algorithm automatically determines the optimal number of clusters.

### Noise Points
Responses that don't fit well into any cluster are marked as "noise" (cluster -1). These might be unique responses or outliers.

### Sentiment Scores
- **Positive (0.1 to 1.0)**: Generally positive sentiment
- **Neutral (-0.1 to 0.1)**: Balanced or neutral sentiment  
- **Negative (-1.0 to -0.1)**: Generally negative sentiment

### Key Terms
The most characteristic words that define each cluster, ranked by TF-IDF importance.

## Customization

The notebook can be easily customized for different analysis needs:

- **Text preprocessing**: Modify language, stemming, or stop words
- **Clustering parameters**: Adjust sensitivity and minimum cluster sizes
- **Visualization**: Change colors, layouts, or add new chart types
- **Export formats**: Add JSON, Excel, or database exports

## Troubleshooting

### Common Issues

1. **"No module named 'hdbscan'"**
   - Run: `pip install hdbscan`

2. **Google API Authentication Error**
   - Ensure `credentials.json` is in the correct location
   - Check that Forms API is enabled in Google Cloud Console

3. **"Form not found" Error**
   - Verify the form ID is correct
   - Ensure the form is shared appropriately
   - Check that your Google account has access to the form

4. **Empty Results**
   - Verify the form has responses
   - Check form permissions
   - Ensure text fields contain analyzable content

## Requirements

- Python 3.8+
- Google Cloud Project with Forms API enabled
- Valid Google Form with responses
- Internet connection for API calls

## Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.

## License

This project is open source and available under the MIT License.

## 🔄 Modular Workflow Benefits

The 4-part structure provides several advantages:

- **🎯 Focused execution**: Each notebook has a single responsibility
- **🔄 Resumable process**: Can restart from any part if needed  
- **🐛 Easier debugging**: Issues are isolated to specific steps
- **⚡ Faster iterations**: Modify one part without re-running everything
- **📊 Intermediate inspection**: Can examine data at each stage
- **🔧 Customizable**: Easy to modify individual components

## 📋 Data Flow

```
Google Forms API → Part 1 → raw_form_responses.pickle
                           ↓
               Part 2 → preprocessed_data.pickle  
                           ↓
               Part 3 → clustered_data.pickle
                           ↓
               Part 4 → final_analysis_results.csv
                        cluster_summary_report.txt
```
