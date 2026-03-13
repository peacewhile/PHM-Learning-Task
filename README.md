# PHM-Learning-Task
# NGAFID 航空维护事件二分类检测

基于论文《A Large-Scale Annotated Multivariate Time Series Aviation 
Maintenance Dataset from the NGAFID》，使用 MiniRocket 模型实现
维护事件二分类检测（维护前 vs 维护后航班）。

---

## 项目简介

本项目使用 NGAFID 数据集的 2days 子集，包含 19 类维护事件，
通过 MiniRocket 时序分类模型实现二分类检测，
并采用五折交叉验证评估模型性能。

---

## 环境配置

### 一键安装依赖
pip install -r requirements.txt

### 主要依赖库
- tsai
- scikit-learn
- seaborn
- matplotlib
- numpy
- pandas
- tqdm
- fastai
- gdown

---

## 数据集

使用 NGAFID 2days 子集（论文 Section 3.2 基准子集）
- 航班数量：11446 条
- 特征数量：23 个传感器
- 标签：before_after（1=维护前，0=维护后）
- 五折划分：fold 字段 0~4

数据集通过 Google Drive 公开共享，运行 notebook 
第一个单元格会自动下载，无需手动操作。

---

## 运行方式

1. 点击下方按钮在 Google Colab 中打开：
   [https://colab.research.google.com/github/peacewhile/PHM-Learning-Task/blob/main/NGAFID_DATASET_MINIROCKET_EXAMPLE8.ipynb]

2. 运行时 → 全部运行

3. 等待约 1~2 小时完成五折训练

---

## 模型说明

### 为什么选择 MiniRocket
- 专为时间序列分类设计
- 计算效率高，适合多变量时序数据
- 在多个时序分类基准上达到最优性能

### 关键参数
| 参数 | 值 | 说明 |
|---|---|---|
| target_len | 200 | 时序统一长度（内存限制） |
| chunksize | 32 | 特征提取批大小 |
| epochs | 200 | 训练轮数 |
| learning_rate | 2.5e-5 | 学习率 |
| random_seed | 42 | 随机种子（保证可复现） |

---

## 评估指标

选择 **ROC-AUC** 为主要指标，**F1** 为辅助指标。

### 选择理由
- 数据集存在类别不平衡，准确率具有误导性
- ROC-AUC 不受类别不平衡影响
- F1 重点关注少数类（维护前航班）的检测效果

### 五折交叉验证结果
| Fold | Accuracy | F1 | ROC-AUC |
|---|---|---|---|
| Fold 0 | - | - | - |
| Fold 1 | - | - | - |
| Fold 2 | - | - | - |
| Fold 3 | - | - | - |
| Fold 4 | - | - | - |
| **均值** | - | - | - |
| **标准差** | - | - | - |

（运行完成后填入实际结果）

---

## 结果可视化

训练完成后自动生成三张图表：
- fold_metrics.png：五折指标柱状图
- confusion_matrix.png：混淆矩阵（Fold 4）
- metrics_summary.png：均值±标准差汇总图

---



## AI 协作说明

本项目使用 Claude AI 辅助开发，详细的 AI 协作过程、
Prompt 记录及学生贡献标注见 AI协作日志.md。

---

## 参考文献

Yang, H., et al. "A Large-Scale Annotated Multivariate Time 
Series Aviation Maintenance Dataset from the NGAFID." 
数据集仓库：https://github.com/hyang0129/NGAFIDDATASET
