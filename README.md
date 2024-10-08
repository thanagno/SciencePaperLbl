# PDF Processing and Classification Script

This project is about a response on Captonomy [assignment](https://github.com/Captonomy/assessment/tree/main/ml-engineer) using a Python
script that processes scientific PDFs, extracts metadata such as titles and authors, and classifies the papers into predefined 
categories using zero-shot classification. The script cross-checks the extracted information with a provided CSV file and outputs 
the results in JSON format.

## Prerequisites

Before running the script, ensure that you have the following installed:

- Python 3.7 or higher
- A machine with a GPU (optional but recommended for faster classification)
- Libraries:
  - `PyMuPDF` (for PDF processing)
  - `transformers` (for zero-shot classification)
  - `pandas` (for CSV handling)
  - `rapidfuzz` (for string comparison)
  - `tqdm` (for progress tracking)
  - `zipfile` (for handling ZIP files)
  - `torch` (for PyTorch operations)
  
You can install the required libraries using the following command:
```bash
pip install PyMuPDF transformers pandas rapidfuzz tqdm torch
```

## Directory Structure

Before running the script, ensure that the following files are placed in the correct directory structure:

```
/your-directory/
|-- Captonomy-assessment/
    |-- ICDAR2024_papers.zip         # ZIP file containing the PDFs to process
    |-- ICDAR 2024 paper list.csv    # CSV file containing the titles and authors
    |-- main.ipynb            # Python script to run
```

## Files

### 1. `ICDAR2024_papers.zip`
This ZIP file contains the PDFs of the papers to be processed. Each PDF file will have its metadata (title, authors, etc.) extracted and processed.

### 2. `ICDAR 2024 paper list.csv`
This CSV file contains a list of paper IDs, authors, and titles. It is used to cross-check the extracted information from the PDFs.

### 3. `classification_results.json`
This file will store the results after processing the PDFs and classifying them into predefined categories. The categories are:

- Tables
- Classification
- Key Information Extraction
- Optical Character Recognition (OCR)
- Datasets
- Document Layout Understanding
- Others

The file will contain metadata about each paper, including its title, authors, and the assigned category.

### 4. `assignment_captonomy.pdf`
This file is a short report on the project as well as the procedure followed including future work to be done.

## Configuration

Ensure the correct file paths are set up in the script:

```python
file_path = "/content/drive/MyDrive/Colab Notebooks/Captonomy-assesment/"
zip_file_path = file_path + 'ICDAR2024_papers.zip'
csv_file_path = file_path + 'ICDAR 2024 paper list.csv'
output_json_path = os.path.join(file_path, 'classification_results.json')
```

Update the `file_path` variable to point to the location where your ZIP and CSV files are stored.

## Running the Script

1. Open a terminal and navigate to the folder where the script is located.

2. Run the script using iPython:

### What the Script Does

1. Extracts text and metadata (titles, authors, keywords, etc.) from each PDF in the `ICDAR2024_papers.zip` file using `spaCy`.
2. Uses a zero-shot classification model (`facebook/bart-large-mnli`) to classify the papers into predefined categories.
3. Cross-checks the extracted metadata with the `ICDAR 2024 paper list.csv` file to verify the titles and authors.
4. Outputs the results into the `classification_results.json` file.

### Output Example

An example of the output in `classification_results.json` might look like:

```json
{
    "classification": [
        {
            "originalFileName": "0001.pdf",
            "title": "A Novel Approach to Document Analysis",
            "authors": ["John Doe", "Jane Smith"],
            ...
        }
    ],
    "keyInformationExtraction": [...],
    "datasets": [...],
    "others": [...]
}
```

## Logging and Debugging

The script prints detailed progress and debug information in the terminal, including:

- The names of processed files.
- Extracted titles and authors.
- Assigned categories.
- Cross-check results against the CSV data.

## Success Rate

At the end of the script, the success rate of matching the extracted metadata with the CSV file is displayed, along with the 
total number of processed PDFs.