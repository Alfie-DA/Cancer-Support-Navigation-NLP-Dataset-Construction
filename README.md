# Cancer Support Navigation: NLP Dataset Construction

An NLP and web-scraping project that builds a structured cancer-navigation dataset from publicly available Dutch healthcare and cancer-information websites. The dataset is designed to support future patient-navigation tools by connecting common patient questions with relevant source content, English translations, and actionable metadata.

## Project overview

People navigating cancer care often need clear information about referrals, waiting times, treatment decisions, second opinions, support services, and communication with healthcare professionals. This project creates a structured resource to help organise that information.

The workflow:

1. Collects paragraph-level content from selected Dutch cancer and healthcare websites.
2. Matches patient-navigation questions to the most relevant source passage using semantic similarity.
3. Translates matched Dutch content into English.
4. Adds navigation metadata, including patient-journey stage, stakeholder, suggested next step, similarity score, and priority.
5. Exports the final dataset to Excel for review and reporting.

> This project is for information-retrieval and research purposes only. It is not a substitute for professional medical advice, diagnosis, or treatment.

## Key capabilities

- Web scraping with `requests` and Beautiful Soup
- Semantic search using the `all-MiniLM-L6-v2` SentenceTransformer model
- Dutch-to-English translation using the DeepL API
- Similarity-score-based relevance prioritisation
- Patient-navigation metadata classification
- Exploratory analysis of retrieval quality, patient-journey coverage, and source organisations
- Excel dataset export

## Data pipeline

```text
Patient navigation questions
          ↓
Dutch healthcare and cancer-information websites
          ↓
Paragraph extraction and cleaning
          ↓
Semantic similarity matching
          ↓
English translation and short summary
          ↓
Metadata enrichment and quality checks
          ↓
Cancer navigation dataset (.xlsx)
```

## Output dataset

Each row represents a patient question and its best-matching source passage. The Excel output includes:

| Field | Description |
| --- | --- |
| Source Organisation | Organisation associated with the selected source page. |
| Source Title and URL | Traceable source information for review. |
| Scrape Date | Date the web content was collected. |
| Topic and Question | Navigation category and original patient question. |
| Matched Dutch Text | Most semantically similar source passage. |
| English Translation | DeepL translation of the matched passage. |
| Summary / Answer Text | Short extractive summary of the translated passage. |
| Similarity Score and Priority | Retrieval-confidence indicator and High/Medium/Low category. |
| Patient Journey Stage | Navigation stage such as referral, diagnosis, treatment, support, or general. |
| Stakeholder and Action / Next Step | Suggested responsible party and next action. |

## Exploratory analysis

The notebook evaluates the dataset through:

- Summary statistics for semantic similarity scores
- Distribution of retrieval priority
- Patient-journey stage coverage
- Source-organisation frequency
- Manual review of the highest- and lowest-scoring matches

The results show that high semantic-similarity scores still require human review. This is especially important in a healthcare context, where a plausible passage may not fully answer a patient’s specific question.

## Technologies

- Python
- pandas
- requests and Beautiful Soup
- SentenceTransformers
- DeepL API
- Matplotlib
- openpyxl

## Project structure

```text
.
├── CSN_Employer_Project.ipynb       # Main scraping, NLP, and EDA workflow
├── reports/
│   └── CSN_Patient_Navigation_Project_Report.pdf
├── outputs/
│   └── Cancer_Navigation_Dataset.xlsx
├── visualizations/
│   ├── match_priority_distribution.png
│   ├── patient_journey_stages.png
│   └── source_organisation_frequency.png
└── README.md
```

## Getting started

1. Create a Python environment.
2. Install the required packages:

```bash
pip install pandas requests beautifulsoup4 sentence-transformers deepl matplotlib openpyxl
```

3. Create a DeepL API key and keep it private.
4. Store the key in an environment variable, rather than directly in the notebook:

```bash
export DEEPL_AUTH_KEY="your-api-key"
```

5. In the notebook, initialise the translator with:

```python
import os
import deepl

translator = deepl.Translator(os.environ["DEEPL_AUTH_KEY"])
```

6. Run the notebook from top to bottom. The generated dataset is exported as an Excel workbook.

## Responsible use and limitations

- Website content can change, so the collection date and source URL should always be retained.
- Scraping must respect each website’s terms of use, robots.txt guidance, and rate limits.
- Semantic similarity indicates textual closeness, not medical accuracy or completeness.
- Machine translation and automatic summaries require human review before any patient-facing use.
- Source content and the generated dataset are not included in this repository unless sharing permissions allow it.

## Future improvements

- Add source-specific retrieval rules and content-quality checks.
- Use human reviewers to label retrieval relevance and evaluate the model.
- Improve patient-journey classification with a trained classifier or richer rules.
- Add citations, versioning, and duplicate-content detection.
- Build a retrieval-augmented chatbot only with clinical governance, safety review, and clear escalation routes.

## Author

Solomon Alfred
