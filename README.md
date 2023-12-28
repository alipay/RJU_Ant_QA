# RJUA-QADatasets: Ant-Renji Urology Specialty QA Dataset
[查看中文版本](README_cn.md)
## Dataset Overview

The RJUA-QA (RenJi hospital department of Urology and Antgroup collaborative Question and Answer dataset) is an innovative medical urology specialty QA inference dataset. This dataset is a collaborative creation by the AntGroup Medical LLM (Large Language Model) team and the expert team from the Department of Urology at Renji Hospital, affiliated with Shanghai Jiao Tong University School of Medicine. The development of this dataset aims to transform real clinical patient data into virtual patient clinical dialogues, presented in a Q-context-A (Question-context-Answer) format. The dataset's production involves a deep collaboration between AI technology and expert teams, ensuring high efficiency and accuracy. **The case data in this dataset are written by professional doctors based on clinical experience, hence not involving any personal privacy of patients and doctors**.

The RJUA-QA dataset contains 2132 Q&A pairs. Each pair is composed of a question (Question) written by doctors based on clinical experience, an answer (Answer) provided by experts, and related reasoning context (Context). The context information is derived from Chinese guidelines for the diagnosis and treatment of urological and andrological diseases. The dataset includes urological disease data collected from 2019 to 2023, covering various medical scenarios such as outpatient diagnosis, emergency rescue, hospital surgery, and daily health education. It ensures comprehensiveness and depth across multiple dimensions. The dataset focuses on 10 sub-specialties in urology, including but not limited to urological tumors, stones, prostate diseases, male health, urinary control disorders, urinary tract reconstructive surgery, pediatric urological diseases, and kidney transplantation, covering over 97.6% of urology patients. Constructed by the professional medical team of Renji Hospital's Department of Urology, the RJUA-QA dataset ensures the authenticity and accuracy of the data and provides deep practical value in real medical environments.

## Dataset Features and Value

- **Real Clinical Background**: The data come from virtual cases written by clinical experts based on consultation experience, making the dataset more realistic and ensuring data privacy.
- **Diversity**: The questions cover multiple aspects of urology, accounting for 95% of all urological diseases.
- **Interpretability**: The dataset provides detailed specialty evidence and reasoning processes.

This dataset aims to enhance the capabilities of large language models in medical diagnostic reasoning and serves as a benchmark for applications in serious and controllable scenarios. The team will continue to optimize the dataset, supporting research and application of artificial intelligence in the medical field.

## Dataset Annotation Process and Standards

### Data Cleaning
The main purpose is to remove irrelevant or redundant information from the data, including correcting spelling errors, unifying formats, deleting duplicate data, and handling missing or incomplete data entries.

### Data Denoising
The goal is to identify and eliminate any noise in the data that might affect subsequent analysis. This noise mainly arises from errors during data collection, transmission, or processing. Methods like filtering, outlier detection, and statistical approaches are used to smooth the data.

### Structured Data Extraction
The aim is to systematically organize and transform the data into formats suitable for analysis or model development. This includes parsing text data to extract relevant fields, converting unstructured or semi-structured data into tabular formats, and classifying or encoding the data to simplify subsequent processing steps.

### Context Matching
1. Under the guidance of professional doctors, manually extract (rough recall) text fragments potentially related to disease diagnosis and treatment from guideline books as context candidates.
2. For each QA data, for each context candidate related to its disease, concatenate [Q, A, context candidate] text fragments and use a large language model to judge the match (ask ChatGPT if the context fragment is directly related to the QA dialogue or serves as a basis for the doctor's answer); the matched context candidate becomes the dataset's context.
3. In some data, randomly select context candidates for non-related diseases for the aforementioned QA-context matching, mixing matched contexts into the context of that QA as distractors to appropriately increase task difficulty.
4. Perform manual verification of the data, adding any missed context recalls.

## Usage Instructions

### Data Format

Questions, documents, and answers are all stored in plain text format, provided in JsonLines format.

The dataset is divided into 3 files, with the training set and validation set used for model training and validation, and the test set used for model inference metric evaluation.

- **train**: Training set
- **valid**: Validation set
- **test**: Test set

Specific fields for each file include:

- **Data ID**: id
- **Question**: Question
- **Context**: Reference text
- **Answer**: Answer
- **Disease**: Diagnosed disease
- **Advice**: Diagnostic and therapeutic advice

### Inference Evaluation Metrics

The evaluation task designed for this dataset mainly aims to compare the consistency of the model's output with the answers of specialist doctors, based on virtual patient questions and doctors' answers. The model needs to refer to the medical knowledge provided by the doctor as context. The specific evaluation metrics are as follows:

1. **F1 Score**:
   - Precision (P): 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;P=\frac{TP}{TP+FP}" alt="P = \frac{TP}{TP + FP}" /> </center> 

   - Recall (R):
   <center>  <img src="https://latex.codecogs.com/svg.latex?\small&space;R=\frac{TP}{TP+FN}" alt="R = \frac{TP}{TP + FN}" /> </center> 

   - F1 Score: 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;F1=\frac{2PR}{P+R}" alt="F1 = \frac{2PR}{P + R}" /> </center> 
   
   - Average F1 Score: 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;F1=\text{average}\left(\frac{2\times{F1_{\text{disease}}}+F1_{\text{advice}}}{3}\right)" alt="F1 = \text{average}\left(\frac{2 \times F1_{\text{disease}} + F1_{\text{advice}}}{3}\right)" /> </center> 

2. **RougeL Score**:
   - P (Precision): 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;P=\frac{\text{LCS}(S1,S2)}{\text{len}(S1)}" alt="P = \frac{\text{LCS}(S1, S2)}{\text{len}(S1)}" /></center> 

   - R (Recall): 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;R=\frac{\text{LCS}(S1,S2)}{\text{len}(S2)}" alt="R = \frac{\text{LCS}(S1, S2)}{\text{len}(S2)}" /></center> 

   - Rouge-L: 
   <center> <img src="https://latex.codecogs.com/svg.latex?\small&space;\text{Rouge-L}=\frac{2PR}{P+R}" alt="\text{Rouge-L} = \frac{2PR}{P + R}" /></center> 

### Citation

If you find our work helpful and have used our dataset, please cite the following description. We will continue to optimize the dataset and update the citable arXiv paper.

```bibtex
@misc{lyu2023rjuaqa,
      title={RJUA-QA: A Comprehensive QA Dataset for Urology}, 
      author={Shiwei Lyu and Chenfei Chi and Hongbo Cai and Lei Shi and Xiaoyan Yang and Lei Liu and Xiang Chen and Deng Zhao and Zhiqiang Zhang and Xianguo Lyu and Ming Zhang and Fangzhou Li and Xiaowei Ma and Yue Shen and Jinjie Gu and Wei Xue and Yiran Huang},
      year={2023},
      eprint={2312.09785},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

### Download

You can download the dataset from the project [QJUA-QA](http://openkg.cn/dataset/rjua-qadatasets) at OpenKG.

For any questions or suggestions about the dataset, please contact us at: chichenfei@renji.com, huangyiran@renji.com, hongbo.chb@antgroup.com, zhanying@antgroup.com

**Note**: When using the dataset, please ensure compliance with relevant laws, regulations, and data privacy policies.