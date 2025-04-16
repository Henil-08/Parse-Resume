# 📄 Resume Parser

A Resume extractor to pull relevant details from CVs in PDF format, and match them against the job descriptions from the Hugging Face dataset.

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/Henil-08/Parse-Resume.git
cd Parse-Resume
```

### 2. Make Sure Python 3.10 is Installed

You can check your Python version using:

```bash
python --version
```

### 3. Setup Options

You can choose to set up the project using Poetry or Conda.

#### Using Poetry

##### For macOS:

(Optional if python 3.10 is not installed)
```bash
brew install python@3.10 
brew link python@3.10 --force
```

```bash
pip install poetry

poetry env use python3.10
poetry install
```

##### For Windows:
1.	Download and install Python 3.10.
2.	Add Python 3.10 to your system PATH.
3.	Install Poetry: `pip install poetry`
4.	Set up the virtual environment and install dependencies:

```bash
poetry env use python3.10
poetry install
```

#### Using Conda

```bash
conda create -n resume-parser python=3.10
conda activate resume-parser

pip install -r requirements.txt
```

## Datasets

The required datasets are already downloaded and stored in the data/ folder of this repository. However, if you still wish to download them manually, here are the sources:

1. Resume Dataset: https://www.kaggle.com/datasets/snehaanbhawal/resume-dataset?resource=download
2. Job Description Dataset: https://huggingface.co/datasets/jacob-hugging-face/job-descriptions

## Notebooks

1. PDF Extractor (`01_data_extraction.ipynb`):
    - Utilized the pdfplumber library to extract raw text from resume PDFs.
    - Applied Python regular expressions to extract the Skills and Education sections from the extracted text.
    - The relevant extracted information was saved into a CSV file named `extracted_resume.csv`
    - Regular expressions were somewhat effective in extracting Skills and Education, but they lacked generalization across resumes with varying formats. Extracting Experience information proved to be particularly difficult. Designing a regex pattern capable of handling multiple headers (e.g., multiple experiences, company names, dates) was not straightforward.
    - A potential solution is to train a Custom Named Entity Recognition (NER) model.
	- This would require creating or acquiring a custom annotated dataset labeled with entities such as Skills, Education, and Experience.
	- Such a model would offer greater flexibility and generalization across different resume formats.

2. CV-JD Matching (Notebooks from 03-05)
    - Selected 15 Job Descriptions (JDs) from the Hugging Face dataset for this project.
	- Performed basic text cleaning on extracted resumes, including converting to lowercase and removing punctuation, emails, and phone numbers.
	- Applied tokenization and embeddings for both JDs and CVs using DistilBertModel, GPT-2 and LlaMa1.1 from the transformers library.
	- Utilized cosine_similarity from the sklearn library to match CVs to JDs.
	- Extracted the top-5 candidates for each Job Description based on the highest similarity scores.