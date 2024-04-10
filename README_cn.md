# RJUA-QADatasets: 蚂蚁-仁济泌尿专科QA数据集
[English Version](README.md)
## 数据集概况

RJUA-QA（RenJi hospital department of Urology and Antgroup collaborative Question and Answer dataset）是一个创新性的医疗泌尿专科QA推理数据集。这一数据集是由蚂蚁集团医疗大模型团队（AntGroup Medical LLM）与上海交通大学医学院附属仁济医院泌尿科（Department of Urology, Shanghai Jiao Tong University School of Medicine Affiliated Renji Hospital）的专家团队联手打造。数据集的开发旨在将真实临床经验中的患者数据转化为虚拟的患者临床对话，以问答对(Q-context-A)的形式展现，数据集的生产由AI技术和专家团队深度合作，提高效率的同时数据集的准确性也有严格的保证。**本数据集的病例数据由专业医生的根据临床经验编写而成，因此不涉及任何医患个人隐私**。

RJUA-QA数据集共含2132个问答对，每对问答由医生根据临床经验编写的问题(Question)、专家提供的回答(Answer)以及相关的推理上下文(Context)构成，这些上下文信息源自中国泌尿外科和男科疾病诊断治疗指南。本数据集包含了从2019年至2023年期间收集的泌尿科疾病数据，这些数据涵盖了门诊诊断、急诊抢救、住院手术及日常科普等多种医疗情境，确保了数据集在多个维度上的全面性和深度。数据集专注于泌尿科的10个子专业领域，包括但不限于泌尿系肿瘤、结石、前列腺疾病、男性健康、尿控制障碍、泌尿道修复手术、儿童泌尿疾病和肾脏移植，涵盖了泌尿科就诊97.6%以上患者的情况。由上海仁济医院泌尿科的专业医生团队参与构建，RJUA-QA数据集不仅确保了数据的真实性和准确性，还提供了在实际医疗环境中的深度应用价值。

## 数据集特点与价值

- **真实临床背景**：数据来源于由临床专家根据问诊经验编写编写而来的虚拟病例，数据集更加真实，同时也保证了数据的隐私性。
- **多样性**：问题涵盖了泌尿专科的多个方面，占比泌尿专科全病种的95%。
- **可解释性**：提供详细的专科证据和推理过程。

本数据集旨在提高大型语言模型在医疗诊断推理方面的能力，并作为在严肃可控场景下应用的评测基准。后续团队将持续优化数据集，为人工智能在医疗领域的研究与应用提供有力支持。

## 数据集标注流程与标准

### 数据清洗
主要目的是去除数据中的不相关或冗余的信息，包括纠正拼写错误、统一格式、删除重复数据以及处理缺失或不完整的数据条目等。

### 数据去噪
主要目的是识别并消除数据中可能影响后续分析的任何噪声。这些噪声主要来自于数据收集、传输或处理过程中的错误，采用诸如过滤、异常值检测和统计方法等手段来平滑数据。

### 结构化数据抽取
主要目的是将数据系统地组织和转换成适合分析或模型开发的格式，主要包括解析文本数据以提取相关字段，将非结构化或半结构化数据转换成表格格式，以及对数据进行分类或编码以简化后续处理步骤。

### Context匹配
1. 根据专业医生的指导，从指南书籍材料人工抽取（粗召回）一些可能与疾病诊疗相关的文本片段，作为context候选项。
2. 对一条QA数据，对其相关疾病的每一条context候选项，都拼接【Q、A、context候选项】文本片段，采用大语言模型进行匹配判断（问ChatGPT该context片段是否与该问答对话直接相关或为医生回答的依据）；将匹配的context候选项作为数据集的context。
3. 在一些数据中，随机选择非相关疾病的context候选项也进行如上述的QA-context匹配，将匹配到的context也混合至上述该条QA的context中，作为干扰项适当提高任务难度。
4. 对数据进行人工校验，补充漏召回的context。


## 使用说明

### 数据格式

问题、文档和答案均以纯文本形式存储，以JsonLines格式提供。

数据集中划分为3个文件，其中训练集和验证集用于模型训练和验证，测试集用于模型推理指标评测。

- **train**：训练集
- **valid**: 验证集
- **test**: 测试集

每个文件的具体字段包括：

- **数据标号**：id
- **Question**: 问题
- **Context**: 参考文本
- **Answer**: 答案
- **Disease**：诊断疾病
- **Advice**：诊疗建议

### 推理评估指标

本数据集设计的评测任务主要目标是针对基于虚拟患者问题以及专科医生回答，待评测模型需参考医生给出的相关医学知识作为context，比较模型产出的回答结果与专科医生回答结果的一致性。具体评估指标设计如下：

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

### 引用

如果你觉得我们的工作有帮助，使用了我们的数据集，请引用下列说明。后续我们会持续优化数据集，并更新可引用的arxiv论文。

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
### 数据集下载

您可以在OpenKG的[QJUA-QA](http://data.openkg.cn/dataset/rjua-qadatasets)下载本数据集

如有任何关于数据集的问题或建议，请通过以下方式与我们联系：chichenfei@renji.com，huangyiran@renji.com, hongbo.chb@antgroup.com , zhanying@antgroup.com

**注意**：在使用数据集时，请确保遵循相关法律法规和数据隐私政策。