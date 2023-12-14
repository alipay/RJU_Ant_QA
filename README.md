# RJUA-QADatasets: 蚂蚁-仁济泌尿专科QA数据集

## 数据集概况

RJUA-QA（RenJi hospital department of Urology and Antgroup collaborative Question and Answer dataset）是一个创新性的医疗泌尿专科QA推理数据集。这一数据集是由蚂蚁集团医疗大模型团队（AntGroup Medical LLM）与上海交通大学医学院附属仁济医院泌尿科（Department of Urology, Shanghai Jiao Tong University School of Medicine Affiliated Renji Hospital）的专家团队联手打造。数据集的开发旨在将真实临床经验中的患者数据转化为虚拟的患者临床对话，以问答对(Q-context-A)的形式表现。此过程涉及AI技术和专家团队的深度合作，严格保障不涉及任何医患个人隐私。

RJUA-QA数据集共含2132个问答对，每对问答由改写自患者临床病例的问题(Question)、专家提供的回答(Answer)以及相关的推理上下文(Context)构成。这些上下文信息源自中国泌尿外科和男科疾病诊断治疗指南。本数据集的内容丰富，包含了从2019年至2023年期间收集的泌尿科疾病数据。这些数据涵盖了门诊诊断、急诊抢救、住院手术及日常科普等多种医疗情境，确保了数据集在多个维度上的全面性和深度。专注于泌尿科的10个子专业领域，包括但不限于泌尿系肿瘤、结石、前列腺疾病、男性健康、尿控制障碍、泌尿道修复手术、儿童泌尿疾病和肾脏移植，该数据集涵盖的病种占泌尿科就诊患者的高达97.6%。由上海仁济医院泌尿科的专业医生团队参与构建，RJUA-QA数据集不仅确保了数据的真实性和准确性，还提供了在实际医疗环境中的深度应用价值。

## 数据集特点与价值

- **真实临床背景**：数据来源于专科医生经验改写的虚拟患者数据，覆盖近5年科室专家临床经验，具有很高的现实意义和应用价值。
- **多样性**：问题涵盖了泌尿专科的多个方面，占比泌尿专科全病种的95%，有助于提升模型应用的泛化能力。
- **可解释性**：提供详细的专科证据和推理过程，有助于分析模型的推理逻辑，提高可解释性。

本数据集旨在提高大型语言模型在医疗诊断推理方面的能力，并作为在严肃可控场景下应用的评测基准。我们将详细介绍数据集的构建过程、特点及统计分析，并全面评测了行业和通用大模型在该数据集上的性能，后续团队将持续优化数据集，为人工智能在医疗领域的研究与应用提供有力支持。

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
   - Precision (P): \( P = \frac{TP}{TP + FP} \)
   - Recall (R): \( R = \frac{TP}{TP + FN} \)
   - F1 Score: \( F1 = \frac{2PR}{P + R} \)
   - Average F1 Score: \( F1 = \text{average}\left(\frac{2 \times F1_{\text{disease}} + F1_{\text{advice}}}{3}\right) \)

2. **RougeL Score**:
   - P (Precision): \( P = \frac{\text{LCS}(S1, S2)}{\text{len}(S1)} \)
   - R (Recall): \( R = \frac{\text{LCS}(S1, S2)}{\text{len}(S2)} \)
   - Rouge-L: \( \text{Rouge-L} = \frac{2PR}{P + R} \)

### 引用

如果你觉得我们的工作有帮助的话，使用了我们的数据集，请引用下列说明，后续我们会持续优化数据集，并更新可引用的arxiv论文。
> comming soon.

如有任何关于数据集的问题或建议，请通过以下方式与我们联系：chichenfei@renji.com，huangyiran@renji.com, hongbo.chb@antgroup.com , zhanying@antgroup.com

**注意**：在使用数据集时，请确保遵循相关法律法规和数据隐私政策。

