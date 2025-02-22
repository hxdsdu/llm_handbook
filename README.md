# 第一部分：基础知识

## 1、机器学习

**机器学习（Machine Learning, ML）** 是人工智能（AI）的一个子领域，旨在通过数据和算法让计算机系统具备从经验中学习的能力，而无需显式编程。机器学习的核心思想是通过数据训练模型，使模型能够自动识别模式、做出预测或决策。

### 1.1 **机器学习的定义**

机器学习是一种通过数据训练模型，使计算机系统能够自动改进性能的技术。具体来说：

1. **输入**：数据（如文本、图像、数值等）。
2. **输出**：预测、分类、决策或其他任务结果。
3. **目标**：通过训练，使模型在未见过的数据上也能表现良好。

### 1.2 **机器学习的核心要素**

1. **数据**：
   1. 训练模型的基础，通常分为训练集、验证集和测试集。
   2. 数据质量直接影响模型性能。
2. **模型**：
   1. 数学或统计模型，用于从数据中学习模式。
   2. 例如：线性回归、决策树、神经网络等。
3. **算法**：
   1. 用于训练模型的数学方法。
   2. 例如：梯度下降、反向传播、K-means 等。
4. **损失函数**：
   1. 衡量模型预测与真实值之间的差距。
   2. 例如：均方误差（MSE）、交叉熵损失等。
5. **优化**：
   1. 通过调整模型参数，最小化损失函数。
   2. 例如：梯度下降、Adam 优化器等。

### 1.3 **机器学习的类型**

根据学习方式，机器学习可以分为以下几类：

#### 1.3.1 **监督学习（Supervised Learning）**

###### **1.3.1.1 定义**

有监督学习(Supervised Learning):是机器学习中一种常见的学习范式，其基本思想是利用带有标签的训练数据来训练模型，从而使其能够从输入数据中学习到输入与输出之间的映射关系，然后可以利用这个映射关系对新的未标签数据进行预测。

###### **1.3.1.2 任务**

- 分类（Classification）：预测离散标签（如垃圾邮件分类）。
- 回归（Regression）：预测连续值（如房价预测）。
- 目标检测(Object Detection):在图像或者视频中检测出目标物体的位置和类别。例如自动驾驶中识别出道路上的车辆、行人、交通标志等;或者人脸识别中判断出哪一部分是人脸。
- 序列生成(Sequence Generation):根据输入的序列生成输出的序列，如机器翻译、音乐生成等。
- 序列标注(Sequence Labeling):序列标注是一种常见的机器学习任务其中输入数据通常是序列数据，例如文本、语音、生物信息学等。有监督学习可以对输入的序列中的每个元素进行标签预测，如命名实体识别(NamedEntity Recognition，NER，指自然语言处理中，能从文本中提取如人名、地名、组织名、日期、时间、金额等具有特定意义的实体或实体类别)、语音识别(Speech Recognition)等。

###### **1.3.1.3 常用算法**

- 线性回归、逻辑回归、支持向量机（SVM）、随机森林。

###### **1.3.1.4** 例子

**1. 问题描述**

鸢尾花数据集包含 150 个样本，每个样本有 4 个特征：

- 花萼长度（sepal length）
- 花萼宽度（sepal width）
- 花瓣长度（petal length）
- 花瓣宽度（petal width）

目标是根据这些特征将鸢尾花分为 3 类：

- Setosa
- Versicolor
- Virginica

1. **实现步骤**

加载数据集。

数据预处理。

划分训练集和测试集。

选择模型并训练。

评估模型性能。

进行预测。

3、代码实现

```Python
# 导入必要的库
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# 1. 加载数据集
iris = load_iris()
X = iris.data  # 特征
y = iris.target  # 标签

# 2. 数据预处理（标准化）
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 3. 划分训练集和测试集
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.3, random_state=42)

# 4. 选择模型并训练
model = KNeighborsClassifier(n_neighbors=3)  # 使用 KNN 分类器
model.fit(X_train, y_train)

# 5. 评估模型性能
y_pred = model.predict(X_test)

# 计算准确率
accuracy = accuracy_score(y_test, y_pred)
print(f"模型准确率: {accuracy:.2f}")

# 打印分类报告
print("分类报告:")
print(classification_report(y_test, y_pred, target_names=iris.target_names))

# 打印混淆矩阵
print("混淆矩阵:")
print(confusion_matrix(y_test, y_pred))

# 6. 进行预测
new_sample = [[5.1, 3.5, 1.4, 0.2]]  # 新样本
new_sample_scaled = scaler.transform(new_sample)  # 标准化
predicted_class = model.predict(new_sample_scaled)
print(f"预测类别: {iris.target_names[predicted_class][0]}")
```

4、输出示例

```Python
模型准确率: 0.98
分类报告:
              precision    recall  f1-score   support

      setosa       1.00      1.00      1.00        16
  versicolor       1.00      0.94      0.97        18
   virginica       0.92      1.00      0.96        11

    accuracy                           0.98        45
   macro avg       0.97      0.98      0.98        45
weighted avg       0.98      0.98      0.98        45

混淆矩阵:
[[16  0  0]
 [ 0 17  1]
 [ 0  0 11]]
预测类别: setosa
```

5、其他方法

```Python
# 逻辑回归：
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
# 支持向量机（SVM）
from sklearn.svm import SVC
model = SVC(kernel='linear')
# 随机森林：
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier(n_estimators=100)
```

#### 1.3.2 **无监督学习（Unsupervised Learning）**

###### **定义**

   模型从未标记的数据中学习，目标是发现数据中的结构或模式。

###### **任务**

- 聚类（Clustering）：将数据分组（如客户细分）。
- 降维（Dimensionality Reduction）：减少数据特征数量（如 PCA）。

###### **常用算法**

- K-means、层次聚类、主成分分析（PCA）、t-SNE。

###### 例子

1. **问题描述**

鸢尾花数据集包含 150 个样本，每个样本有 4 个特征：

- 花萼长度（sepal length）
- 花萼宽度（sepal width）
- 花瓣长度（petal length）
- 花瓣宽度（petal width）

目标是将数据从 4 维降到 2 维，以便于可视化和分析。

1. **实现步骤**
   1. 加载数据集。
   2. 数据预处理。
   3. 选择降维算法并应用。
   4. 可视化降维结果。

1. **代码实现**

```Python
# 导入必要的库
from sklearn.datasets import load_iris
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt
import pandas as pd

# 1. 加载数据集
iris = load_iris()
X = iris.data  # 特征
y = iris.target  # 标签

# 2. 数据预处理（标准化）
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 3. 选择降维算法并应用
pca = PCA(n_components=2)  # 降维到 2 维
X_pca = pca.fit_transform(X_scaled)

# 4. 可视化降维结果
df_pca = pd.DataFrame(X_pca, columns=['PC1', 'PC2'])
df_pca['Species'] = y  # 添加标签用于可视化

plt.figure(figsize=(8, 6))
for species, color in zip(iris.target_names, ['red', 'green', 'blue']):
    plt.scatter(df_pca[df_pca['Species'] == iris.target_names.tolist().index(species)]['PC1'],
                df_pca[df_pca['Species'] == iris.target_names.tolist().index(species)]['PC2'],
                color=color, label=species)
plt.xlabel('Principal Component 1 (PC1)')
plt.ylabel('Principal Component 2 (PC2)')
plt.title('PCA of Iris Dataset')
plt.legend()
plt.show()
```

4、输出示例

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MGYzNDQzNmE0OGM2M2M1ZmI2ZGEwNjNkNDQ0ZmZmYTJfOXZmMW1veDN4VjlUOUhxTXVUUzQyVGNVWkh6dUlOS3pfVG9rZW46WDUyb2JSaDFsb2doY2t4Q2U3M2NMUnJ2bjhnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 1.3.3. **半监督学习（Semi-supervised Learning）**

##### **定义**

结合少量标记数据和大量未标记数据进行训练。

##### **应用场景**

数据标注成本高时（如医学图像分析）。

##### 常用算法

**基于标签传播的半监督分类、自训练（Self-training）、半监督 SVM、图半监督学习**

##### 例子

1. ###### **问题描述**

我们使用 **鸢尾花数据集**（Iris Dataset），假设只有少量样本有标签，其余样本的标签未知。目标是通过半监督学习，利用未标记数据提升模型性能。

1. ###### **实现步骤**

- 加载数据集。
- 模拟半监督场景（仅少量样本有标签）。
- 使用半监督学习算法（如标签传播）进行训练。
- 评估模型性能。

###### 3、代码实现

```Python
# 导入必要的库
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.semi_supervised import LabelSpreading
from sklearn.metrics import accuracy_score, classification_report
import numpy as np

# 1. 加载数据集
iris = load_iris()
X = iris.data  # 特征
y = iris.target  # 标签

# 2. 模拟半监督场景
# 假设只有 10% 的样本有标签，其余标签未知
rng = np.random.RandomState(42)
random_unlabeled_points = rng.rand(len(y)) < 0.9  # 90% 的样本标签被掩盖
y_semi_supervised = np.copy(y)
y_semi_supervised[random_unlabeled_points] = -1  # 未标记样本的标签设为 -1

# 打印标记和未标记样本的数量
print(f"标记样本数量: {np.sum(y_semi_supervised != -1)}")
print(f"未标记样本数量: {np.sum(y_semi_supervised == -1)}")

# 3. 数据预处理（标准化）
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 4. 使用标签传播算法进行训练
label_prop_model = LabelSpreading(kernel='knn', n_neighbors=7)
label_prop_model.fit(X_scaled, y_semi_supervised)

# 获取预测标签
y_pred = label_prop_model.transduction_

# 5. 评估模型性能
# 仅在有真实标签的样本上评估
mask = y_semi_supervised != -1
accuracy = accuracy_score(y[mask], y_pred[mask])
print(f"模型准确率: {accuracy:.2f}")

# 打印分类报告
print("分类报告:")
print(classification_report(y[mask], y_pred[mask], target_names=iris.target_names))
```

###### 4、输出示例

```Python
标记样本数量: 15
未标记样本数量: 135
模型准确率: 0.93
分类报告:
              precision    recall  f1-score   support

      setosa       1.00      1.00      1.00         5
  versicolor       0.83      1.00      0.91         5
   virginica       1.00      0.80      0.89         5

    accuracy                           0.93        15
   macro avg       0.94      0.93      0.93        15
weighted avg       0.94      0.93      0.93        15
```

#### 1.3.4. **强化学习（Reinforcement Learning, RL）**

##### **定义**

- 模型通过与环境的交互学习策略，以最大化累积奖励。
- 在强化学习中，Agent通过与环境的相互作用，观察环境的状态(State)，执行

​    不同的动作(Action)，接收环境的反馈(奖励信号，奖励Reward)，并根据反馈来调整其行为     策略(Policy)，从而逐渐学习如何在不同的环境中做出最优的决策。

##### 关键特点

- Environment和State:强化学习中的Agent与Environment进行交互，Agent通过观察Environment的State来感知环境的变化并进行决策。(eg.我们开车的时候与我们所看到的路况进行交互，根据路上的行人、其他汽车、指示牌等的状态，选择怎么去打方向盘。那么整个汽车所在的公路就是Environment，公路上具体的路况就是State)
- Action和Policy:Agent可以采取不同的Action来影响Environment的State。那么在什么样的State下，Agent要采取什么样的Action?Agent是基于一定的策略Policy来选择要执行的Action的，而这个Policy往往是一个以当前State为自变量，要执行的Action为输出的一个函数。(eg.我们在路上怎么打方向盘，就是Action。在什么样的路况下我们会怎么去打方向盘，就是Policy。我们打方向盘这件事情会影响环境的状态;而环境的状态改变又会返回来决定我们该怎么打方向盘。)
- Reward和Goal:环境向Agent提供奖励信号，用于反馈Agent的行为质量3.Agent的目标是通过最大化预期的累积奖励，以此来学习如何做出最佳决策。(eg.路边的其他车会向你打鸣告诉你你开的不好，违规了的话交警会对你处罚，这就是一个负的Reward。你的Goal可能是以最快的速度最安全、不违规的到达目的地，你通过不断的与环境交互，学习出一个最佳的开车Policy，从而实现这个目标。)
- 试错学习和优化:强化学习中的Agent通过与环境的交互来不断学习和优化其策略，这是一个不断试错的过程，State和Action之间的往复交互是强化学习的主体部分，所以是Trial and Error Learning。强化学习的最终目标是一个好的策胳。
- **应用场景**：游戏 AI、机器人控制、自动驾驶。
- **常用算法**：
  - Q-learning、深度 Q 网络（DQN）、策略梯度。

#### 1.3.5. **自监督学习（Self-supervised Learning）**

##### **1. 自监督学习的核心思想**

自监督学习通过设计一种任务，从输入数据中自动生成标签，然后利用这些标签来训练模型。这种任务通常被称为**预训练任务**（pretext task），其目的是让模型学习到数据的通用特征表示。

###### **关键点**

- **自动生成标签**：从数据本身生成标签，无需人工标注。
- **预训练任务**：设计一种任务，使模型能够学习到有用的特征。
- **迁移学习**：将预训练模型迁移到下游任务（如分类、检测等）。

##### **2. 自监督学习的优势**

- **减少对标注数据的依赖**：
  - 自监督学习可以利用大量未标注数据，降低数据标注成本。
- **学习通用特征表示**：
  - 通过预训练任务，模型可以学习到数据的通用特征，适用于多种下游任务。
- **适用于多种领域**：
  - 自监督学习在计算机视觉、自然语言处理、语音处理等领域都有广泛应用。

##### **3. 自监督学习的常见方法**

###### **3.1 计算机视觉中的自监督学习**

- **图像补全（Image Inpainting）**：
  - 任务：遮挡图像的一部分，让模型预测被遮挡的部分。
  - 目标：学习图像的局部结构和全局语义。
- **图像着色（Image Colorization）**：
  - 任务：将灰度图像转换为彩色图像。
  - 目标：学习图像的语义信息。
- **拼图游戏（Jigsaw Puzzles）**：
  - 任务：将图像分割成多个小块，让模型重新排列这些小块的顺序。
  - 目标：学习图像的局部和全局关系。
- **旋转预测（Rotation Prediction）**：
  - 任务：将图像旋转一定角度，让模型预测旋转的角度。
  - 目标：学习图像的旋转不变性特征。

###### **3.2 自然语言处理中的自监督学习**

- **掩码语言模型（Masked Language Model, MLM）**：
  - 任务：随机掩盖文本中的一些词，让模型预测被掩盖的词。
  - 目标：学习上下文相关的词表示。
  - 示例：BERT 模型。
- **下一句预测（Next Sentence Prediction, NSP）**：
  - 任务：给定两个句子，让模型判断它们是否是连续的。
  - 目标：学习句子之间的关系。
  - 示例：BERT 模型。
- **对比学习（Contrastive Learning）**：
  - 任务：通过对比正样本和负样本，学习句子或词的表示。
  - 目标：学习语义相似性。
  - 示例：SimCSE 模型。

###### **3.3 语音处理中的自监督学习**

- **语音预测（Future Timestep Prediction）**：
  - 任务：预测语音信号的下一个时间步。
  - 目标：学习语音的时间依赖性。
- **对比预测编码（Contrastive Predictive Coding, CPC）**：
  - 任务：通过对比正样本和负样本，学习语音的表示。
  - 目标：学习语音的语义信息。

##### **4. 自监督学习的典型模型**

###### **4.1 计算机视觉**

- **SimCLR**：
  - 使用对比学习，通过数据增强生成正样本和负样本。
- **BYOL**：
  - 无需负样本，通过在线和目标网络进行对比学习。
- **SwAV**：
  - 结合对比学习和聚类，学习图像的特征表示。

###### **4.2 自然语言处理**

- **BERT**：
  - 使用掩码语言模型和下一句预测进行预训练。
- **GPT**：
  - 使用自回归语言模型进行预训练。
- **SimCSE**：
  - 使用对比学习，学习句子表示。

###### **4.3 语音处理**

- **wav2vec**：
  - 使用对比预测编码，学习语音的特征表示。
- **HuBERT**：
  - 结合掩码预测和聚类，学习语音的表示。

##### **5. 自监督学习的应用场景**

1. **计算机视觉**：
   1. 图像分类、目标检测、图像分割。
2. **自然语言处理**：
   1. 文本分类、机器翻译、问答系统。
3. **语音处理**：
   1. 语音识别、语音合成、语音情感分析。
4. **多模态学习**：
   1. 结合图像、文本和语音的多模态表示学习。

##### **6. 自监督学习的挑战**

1. **预训练任务设计**：
   1. 如何设计有效的预训练任务，使模型能够学习到有用的特征。
2. **计算资源需求**：
   1. 自监督学习通常需要大量的计算资源和数据。
3. **迁移学习效果**：
   1. 如何将预训练模型有效地迁移到下游任务。

## 2、深度学习

### 2.1 表示/表征

#### 2.1.1 表示/表征(Representation)

表示(Representation)则通常指的是将数据以某种形式进行编码或者表示的方式，可以是在特征空间中的表示，也可以是在其他空间中的表示。在深度学习中，表征通常是由模型自动学习得到的，例如通过神经网络的隐藏层进行特征提取和表示学习(后面讲MLP的时候就会提到)。这种自动学习的表现通常比手工设计的特征更能够捕捉数据中的复杂模式和关系，从而提升模型的性能

#### 2.1.2 局部表示

局部表示，也称为离散表示或符号表示。以颜色表示为例，我们可以用很多词来形容不同的颜色1，除了基本的“红”““蓝“““绿““白“黑”等之外还有很多以地区或物品命名的，比如“中国红““天蓝色"“咖啡色"“琥珀色”等，如果要在计算机中表示颜色，一般有两种表示方法，如果以不同名字来命名不同的颜色，这种表示方式叫作局部表示。局部表示通常可以表示为0ne-hot向量的形式，假设假设所有颜色的名字构成一个词表 ，词表大小为|V|.我们可以用一个|V|维的one-hot问量来表示每一种颜色，在第i种颜色对应的one-hot向量中，第i维的值为1，其他都为0.

**例子 1：颜色编码**

假设有三种颜色：红、绿、蓝。

| 颜色 | One-Hot 编码 |
| ---- | ------------ |
| 红   | [1, 0, 0]    |
| 绿   | [0, 1, 0]    |
| 蓝   | [0, 0, 1]    |

**One-Hot 编码的优缺点**

**优点**：

**简单直观**：易于理解和实现。

**适用于类别型数据**：能够有效处理无序的类别型数据。

缺点：

1)one-hot向量的维数很高(维度爆炸)，且不能扩展，如果有一种新的颜色，我们就需要增加一维来表示;2)不同颜色之间的相似度都为0，因为这些向量全部正交。即我们无法知道“红色“和“中国红”的相似度要高于“红色”和“黑色”的相似度。3）One-Hot 编码的向量通常是稀疏的（大部分元素为 0），可能会影响模型性能。

**Python 实现 One-Hot 编码**

```Python
import pandas as pd

# 创建示例数据
data = {'颜色': ['红', '绿', '蓝']}
df = pd.DataFrame(data)
print(df)
# 使用 Pandas 的 get_dummies 函数进行 One-Hot 编码
df_encoded = pd.get_dummies(df, columns=['颜色'],dtype=int)
print(df_encoded)
```

#### 2.1.3 分布式表示

**分布式表示** 是一种将数据表示为低维、连续向量的方法，其中每个特征不再是独立的，而是通过多个维度的组合来表示。与传统的 One-Hot 编码不同，分布式表示能够捕捉数据之间的语义关系，广泛应用于自然语言处理（NLP）、计算机视觉和推荐系统等领域。

- **核心思想**：
  - 将数据（如单词、图像、用户等）映射到一个低维的连续向量空间中。
  - 每个向量由多个维度组成，每个维度表示某种潜在的特征。
- **特点**：
  - **低维**：向量的维度远小于原始数据的可能取值。
  - **连续**：向量中的每个元素是实数，而不是离散值。
  - **语义相似性**：语义上相似的数据在向量空间中距离较近。

**分布式表示 vs. One-Hot 编码**

| 特性     | One-Hot 编码           | 分布式表示                   |
| -------- | ---------------------- | ---------------------------- |
| 维度     | 高维（维度等于类别数） | 低维（维度远小于类别数）     |
| 向量元素 | 离散值（0 或 1）       | 连续值（实数）               |
| 语义关系 | 无法捕捉语义关系       | 能够捕捉语义关系             |
| 稀疏性   | 稀疏（大部分元素为 0） | 稠密（大部分元素非 0）       |
| 应用场景 | 简单分类任务           | 复杂任务（如 NLP、推荐系统） |

**分布式表示的应用**

**自然语言处理（NLP）**

**词向量（Word Embedding）**：

 将单词映射到低维向量空间。

 示例模型：Word2Vec、GloVe、FastText。

**句子表示**：

 将整个句子映射到向量空间。

 示例模型：BERT、Sentence-BERT。

**计算机视觉**

**图像特征表示**：

 将图像映射到低维向量空间。

 示例模型：卷积神经网络（CNN）的特征提取层。

**多模态表示**：

 将图像和文本映射到同一向量空间。

 示例模型：CLIP。

**推荐系统**

**用户和物品表示**：

 将用户和物品映射到低维向量空间。

 示例模型：矩阵分解（Matrix Factorization）、神经协同过滤（NCF）

**分布式表示的典型模型**

**自然语言处理**

**Word2Vec**：

 通过预测上下文词（CBOW）或预测目标词（Skip-Gram）学习词向量。

**BERT**：

 使用 Transformer 架构和掩码语言模型（MLM）学习上下文相关的词向量。

 实例1

 **使用 Word2Vec 学习词向量**

```Python
# 示例句子
from gensim.models import Word2Vec
# 示例文本数据
sentences = [
    "This is a sample sentence for Word2Vec.",
    "Word2Vec is a popular algorithm for generating word vectors.",
    "It uses the context of words to learn their representations.",
    "Word2Vec can be trained using either the CBOW or Skip-Gram model."
]

# 将文本数据转换为句子列表，每个句子是一个单词列表
sentences = [sentence.lower().split() for sentence in sentences]

# 创建 Word2Vec 模型
model = Word2Vec(sentences, vector_size=100, window=5, min_count=1, workers=4)

# 保存模型
model.save("word2vec.model")

# 加载模型
model = Word2Vec.load("word2vec.model")

# 获取单词的向量表示
word = "word2vec"
vector = model.wv[word]
print(f"Vector for '{word}': {vector}")

# 查找与给定单词最相似的单词
similar_words = model.wv.most_similar(word, topn=5)
Vector for 'word2vec': [-0.00713904  0.00124101 -0.00717672 -0.00224463  0.0037193   0.00583314
  0.00119819  0.00210271 -0.00411038  0.00722534 -0.00630706  0.00464721
 -0.00821997  0.00203648 -0.00497707 -0.00424767 -0.00310898  0.00565523
  0.00579841 -0.00497463  0.00077334 -0.00849575  0.0078098   0.00925732
 -0.0027423   0.00080025  0.00074667  0.00547787 -0.00860609  0.00058445
  0.00686943  0.00223161  0.00112467 -0.00932216  0.00848237 -0.00626413
 -0.00299238  0.00349379 -0.00077261  0.00141131  0.00178201 -0.0068289
 -0.00972482  0.00904056  0.00619806 -0.00691292  0.00340346  0.00020606
  0.00475375 -0.00711997  0.00402695  0.00434745  0.00995735 -0.00447375
 -0.00138924 -0.00731732 -0.00969783 -0.00908027 -0.00102275 -0.00650328
  0.00484972 -0.00616403  0.00251918  0.00073945 -0.00339214 -0.00097924
  0.0099791   0.00914586 -0.00446181  0.00908302 -0.00564175  0.0059309
 -0.00309723  0.00343174  0.00301722  0.00690044 -0.00237387  0.00877502
  0.00758943 -0.00954763 -0.0080082  -0.00763792  0.00292328 -0.00279472
 -0.00692954 -0.00812826  0.0083092   0.00199051 -0.00932804 -0.00479273
  0.00313673 -0.0047132   0.00528087 -0.00423345  0.00264178 -0.00804567
  0.00620991  0.0048189   0.00078721  0.00301345]
Words similar to 'word2vec': [('vectors.', 0.252905011177063), ('trained', 0.20086903870105743), ('or', 0.17511184513568878), ('a', 0.17025089263916016), ('word', 0.1501648873090744)]
```

使用bert获取句子表示

```Python
from sentence_transformers import SentenceTransformer, util
import numpy as np

# 加载预训练的 SBERT 模型
model = SentenceTransformer('bert-base-nli-mean-tokens')  # 使用均值池化策略的 BERT 模型

# 定义需要计算句子表示的句子
sentences = [
    '中午我想吃清蒸鲈鱼',
    '天气预报说明天下雨',
    '食堂的餐饭不好吃',
    '我做了红烧鱼作为中午的饭菜'
]

# 使用预训练的 SBERT 模型的 encode 函数计算句子表示
sentence_embeddings = model.encode(sentences)

# 查看句子表示的维度
print(f"句子表示的维度: {sentence_embeddings.shape}")

# 计算句子之间的余弦相似度
cosine_similarities = util.pytorch_cos_sim(sentence_embeddings, sentence_embeddings)

# 打印句子之间的余弦相似度
print("句子之间的余弦相似度:")
print(cosine_similarities)

# 计算第一句和其他句子之间的余弦相似度
sim_scores = cosine_similarities[0][1:].tolist()
sim_scores = [round(score, 4) for score in sim_scores]

# 打印第一句和其他句子之间的余弦相似度
print("第一句和其他句子之间的余弦相似度:")
for i, score in enumerate(sim_scores):
    print(f"句子1 和 句子{i+2} 的余弦相似度: {score}")
```

输出结果

```Python
句子表示的维度: (4, 768)
句子之间的余弦相似度:
tensor([[1.0000, 0.8021, 0.8164, 0.9414],
        [0.8021, 1.0000, 0.7101, 0.7732],
        [0.8164, 0.7101, 1.0000, 0.8682],
        [0.9414, 0.7732, 0.8682, 1.0000]])
第一句和其他句子之间的余弦相似度:
句子1 和 句子2 的余弦相似度: 0.8021
句子1 和 句子3 的余弦相似度: 0.8164
句子1 和 句子4 的余弦相似度: 0.9414
```

### 2.2  MLP

#### 2.2.1. 基本概念

**定义**：多层感知机（MLP）是一种前馈神经网络，由多个层组成，包括输入层、隐藏层和输出层。

**神经元**：每个层由多个神经元组成，神经元是网络的基本计算单元。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MmIzNDFlOWU2YzZhZjA0ZjE5ZDMyY2ZkYzkyYzFkYTVfbUkzOFRxdlBmSU40cFJMSmVwWDJXVFlNVHJGOWZYNnNfVG9rZW46VUd4cGJNVW1Ob1dDMzF4RFZFb2M1b2dPbldlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

```Python
import numpy as np

# 定义输入和参数
x = np.array([2.0, 3.0])  # 输入
w = np.array([0.5, -1.0])  # 权重
b = 0.1  # 偏置

# 计算加权求和
z = np.dot(x, w) + b
print(f"Weighted Sum (z): {z}")

# 定义 ReLU 激活函数
def relu(z):
    return max(0, z)

# 计算神经元输出
output = relu(z)
print(f"Neuron Output: {output}")
```

**激活函数**：每个神经元的输出通过一个非线性激活函数进行处理，常见的激活函数有 Sigmoid、ReLU 和 Tanh。

#### 2.2.2 网络结构

**输入层**：接收输入数据，每个神经元对应一个输入特征。

**隐藏层**：一个或多个层，用于提取输入数据的高级特征。

**输出层**：生成最终的输出结果，神经元数量取决于任务类型（如分类或回归）。

#### 2.2.3. 前向传播

**输入**：输入数据 X**X** 通过输入层传递。

**加权求和**：每个神经元对输入数据进行加权求和，加上偏置项 b*b*：

z=W⋅X+b*z*=**W**⋅**X**+*b*

**激活函数**：通过激活函数 σ*σ* 处理加权求和的结果：

a=σ(z)*a*=*σ*(*z*)

**输出**：最终输出层的激活结果作为网络的输出。

#### 2.2.4. 损失函数

**定义**：损失函数用于衡量模型预测值与真实值之间的差异。

**常见损失函数**：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDY3NTVjZjg2YTJiNjMwMDc1YmNiZWM5Y2Y5MDY5OTVfeHpkdGE4MkpCa1NUMGp1MkpkdnlnRVZZRmJuUFNsM2dfVG9rZW46UjdMRmJ3QmZsbzNtNjB4QVkxTWNDZXRPbkdlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.2.5 反向传播

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzdmM2FjODI0ZmRlNDVlZTUwYWVjNTljNmVlNDAyY2FfVGxqSFpUTlJjdXI5TzVMdDd6dW93OHdGVVI2Q3pVOVRfVG9rZW46TWRvQ2JzU3FVb0RaRnR4OHBFa2NFcWJwbmFjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.2.6 梯度下降

梯度下降是什么？

梯度下降是深度学习中用来优化模型参数的算法。它的目标是找到使损失函数（即模型预测值与真实值之间的误差）最小的参数值。你可以把它想象成在山谷中寻找最低点的过程。

梯度下降的基本思想

**梯度**：梯度是一个向量，表示函数在某一点的变化率。在深度学习中，梯度告诉我们损失函数在当前参数下的变化方向。

**下降**：沿着梯度的反方向调整参数，逐步减少损失函数的值。

梯度下降的步骤

**初始化参数**：随机选择参数的初始值。

**计算梯度**：计算损失函数对参数的梯度。

**更新参数**：沿着梯度的反方向调整参数。

**重复**：重复步骤2和3，直到损失函数收敛到最小值。

举个例子：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTEzNDA3MjUwZjgzYzk1ZjUzZWMwZjdiNmQ1ZDJjYjVfTklEckpLMlVSN2wyQWVIRjVJWHdmbERkZlNkdThlSDlfVG9rZW46TXBCY2JXeU5yb2Z2Sml4bGJPcGN2SVJUbkJkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDg3MTc5MjAwNzVlMGE4ODEzNTViOTk0YjZkMzdiNmVfcFpLQXRqS093OEZUVjRGMmtTRzJxUko4TGZrNDAycENfVG9rZW46Q0RxWmJiU2p0b1ZrMG54UlJWOGM4TnpTbmZmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MGE1ZjFmZjU4YjMzYjA0YTVhMGI1NjM0ZGUzZTIwMzBfNWprRHhCOVh5R3ZSQzVtdG9lQ0NKTmU0RFZVbWk4bmRfVG9rZW46V20wS2I3S3Uzb2dHMmp4c1l2V2NoZmhvbnhmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWJmOTZhNDRiNmNjZGZiNmYzZGYxZWY0ZGY4MGU5MjhfcER6cmhHN042MmlaQ3NlU0k2RFQ1VW51TjdYMU9aUjBfVG9rZW46S1Y5cWJrNFNHb2VHejV4MGpZZGNoM0FmbmVmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YjkyMTEzMWJiYmRkY2MxNGRiMGIzOGFmYTVjZGE1ZThfUEFldHBxaVI4NkdYN1YybnRmMEYzbmZ6S2NwRzlJSWZfVG9rZW46TGY4TmJQeXRXbzU3c1h4RVozdWN6UWgxblpjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YzYwMDdjZjQwODdjNmExOTRlNTMzODQ4ZTAxNmNjNjRfTWwzckpPWk5yTTJsWnJ4Z2tiN0lyMkV1TTlpQnRSVElfVG9rZW46QTNNd2JHbGVob295cjN4NFJmVmNiSkd4bm1iXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.2.7 梯度消失详解

什么是梯度消失？

梯度消失是指在深层神经网络中，反向传播时梯度值逐渐变小，最终趋近于零，导致参数无法有效更新。

**梯度消失的原因**

**激活函数**：

1.  使用 Sigmoid 或 Tanh 激活函数时，梯度值会被压缩到很小的范围（如 Sigmoid 的梯度在 [0, 0.25] 之间）。

1.  多层叠加后，梯度值会指数级减小。

**网络深度**：

1.  网络层数越多，梯度传播的路径越长，梯度消失的可能性越大。

**权重初始化**：

1.  如果权重初始化不当（如值过小），梯度值也会变小。

梯度消失的影响

**参数无法更新**：

1.  梯度值趋近于零，导致参数几乎不更新。

**训练停滞**：

1.  模型性能无法提升，损失函数不再下降。

**深层网络失效**：

1.  深层网络的优势无法发挥。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTQwMzY1Yzc0NWZkNWU2M2NhNzc4M2VkZWU0ZmMyYWRfNGhiMmM4NDRPNlhnWDNhMjdQc1VwcHZKNDNrVnJvSXVfVG9rZW46R1RmUmJvWk5mbzZnc0l4azlTZGNjUkJvbktmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTEzNjdkNmZhNzJlYTMxMTc1MWIzODNmMTU0ZDkzMTZfUENGc00wdjk1b0ZvWm5abDFFcUhMb2ozTkltMjQ5dHRfVG9rZW46S3F1U2JWaDF3b3BpcGZ4bm05eWN5NTFUbmRoXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDAwNDM2M2E0M2ZjOTRiY2YyYTUzMTQxMmUwYjYzNmRfRmg5QnpCVzBEWmFyQmw4b2FyOU9hQjRGWENRdjdvbFZfVG9rZW46RllvV2IxZU5qbzdsdFV4aGN6cWNQcGx0bmxCXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.2.8 梯度爆炸

是深层神经网络中的常见问题。

主要由网络深度、权重初始化不当、激活函数和学习率过高引起。

应对梯度爆炸的办法

**梯度裁剪**：限制梯度的最大值。

**改进权重初始化**：使用 Xavier 或 He 初始化。

**使用归一化技术**：如批量归一化或层归一化。

**调整学习率**：降低学习率或使用学习率调度器。

**使用合适的激活函数**：如 ReLU、Leaky ReLU 或 ELU。

**使用残差网络**：引入跳跃连接，稳定梯度传播。

**使用自适应优化器**：如 Adam 或 RMSprop。

#### 2.2.6. 训练过程

**初始化**：随机初始化网络权重。

**前向传播**：计算网络的输出。

**计算损失**：使用损失函数计算预测值与真实值之间的差异。

**反向传播**：计算损失函数对权重的梯度。

**更新权重**：使用梯度下降法更新权重。

**重复**：重复上述步骤，直到损失函数收敛或达到预定的训练轮数。

#### 2.2.9 超参数详解

\1. **网络结构相关超参数**

(1) 隐藏层的层数 (`n_layers`)

**定义**：隐藏层的数量。

**作用**：增加层数可以提高模型的表达能力，但也可能导致过拟合和训练难度增加。

**建议**：从 1-3 层开始尝试，根据任务复杂度调整。

(2) 每层的神经元数量 (`hidden_units`)

**定义**：每个隐藏层的神经元数量。

**作用**：神经元数量越多，模型的表达能力越强，但计算成本也越高。

**建议**：通常选择 32、64、128、256 等值，根据数据规模和任务复杂度调整。

(3) 激活函数 (`activation`)

**定义**：用于引入非线性，常见的激活函数有 ReLU、Sigmoid、Tanh 等。

**作用**：激活函数决定了神经元的输出方式。

**建议**：

 **ReLU**：最常用，计算简单且效果好。

 **Sigmoid/Tanh**：适用于输出层或特定任务。

 **Leaky ReLU/ELU**：解决 ReLU 的“死亡神经元”问题。

\2. **优化相关超参数**

(1) 学习率 (`learning_rate`)

**定义**：控制参数更新的步长。

**作用**：学习率过大会导致震荡，过小会导致收敛慢。

**建议**：通常从 0.001 或 0.0001 开始尝试。

(2) 优化器 (`optimizer`)

**定义**：用于更新模型参数的算法。

**常见优化器**：

 **SGD**：随机梯度下降，简单但容易陷入局部最优。

 **Adam**：自适应学习率，通常效果较好。

 **RMSprop**：适用于非平稳目标函数。

**建议**：优先使用 Adam。

(3) 批量大小 (`batch_size`)

**定义**：每次更新参数时使用的样本数量。

**作用**：批量大小影响训练速度和稳定性。

**建议**：通常选择 32、64、128 等值。

\3. **正则化相关超参数**

(1) L2 正则化 (`weight_decay`)

**定义**：在损失函数中加入权重的 L2 范数，防止过拟合。

**作用**：限制权重的大小，使模型更简单。

**建议**：通常设置为 0.0001 或 0.001。

(2) Dropout (`dropout_rate`)

**定义**：在训练过程中随机丢弃一部分神经元。

**作用**：防止过拟合，增强模型的泛化能力。

**建议**：通常设置为 0.2-0.5。

\4. **训练相关超参数**

(1) 训练轮数 (`epochs`)

**定义**：整个数据集被遍历的次数。

**作用**：训练轮数过少可能导致欠拟合，过多可能导致过拟合。

**建议**：根据验证集性能决定是否提前停止。

(2) 早停 (`early_stopping`)

**定义**：当验证集性能不再提升时，提前停止训练。

**作用**：防止过拟合，节省训练时间。

**建议**：设置 `patience` 参数（如 10），表示连续多少轮性能不提升后停止。

\5. **其他超参数**

(1) 初始化方法 (`initialization`)

**定义**：模型参数的初始化方式。

**常见方法**：

 **Xavier/Glorot**：适用于 Sigmoid 和 Tanh。

 **He**：适用于 ReLU。

**建议**：根据激活函数选择合适的初始化方法。

(2) 损失函数 (`loss`)

**定义**：衡量模型预测值与真实值之间的差异。

**常见损失函数**：

 **MSE**：用于回归任务。

 **Cross-Entropy**：用于分类任务。

**建议**：根据任务类型选择合适的损失函数。

#### 2.2.7 例子：mnist手写数据集

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTZiNDc4N2QzY2VkN2Y5ZWIyZDY4NzE1ZTMwYWM1ZTdfd3BWcmM2ekVXRkJtMFg2V0JaSjlMYWNlYmVxS05mcFNfVG9rZW46SVdwaGJpUVpZb3NGc3V4OFFDQWMwYVc5bllkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MmQwZmY0ZGI3MjZmNDdhOGI3NWZjMTI1NmExZTdiYjRfUDQ2V04zWU4yYjl3TmxKbG5LSEoyV0J1bWQ5QlVsZ09fVG9rZW46V092YmJabXVEb0paMEV4b200SGN4OE5FbmNoXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OGRjNGM0NTg4ZmYxMThmNTRiYmYyNGIwNzAxYmYwZDNfaWQxM3RrNERYZmllZjBiZDJGREdzcG1wZTBhUzZPUHJfVG9rZW46THBTcGJJZ1lxb2NtZk14VTZ1ZWN5U3drbnNnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.2.8 numpy实现MLP

```Python
class SimpleNN:
    def __init__(self, input_size, hidden_size, output_size):
        self.W1 = np.random.randn(input_size, hidden_size)
        self.b1 = np.zeros(hidden_size)
        self.W2 = np.random.randn(hidden_size, output_size)
        self.b2 = np.zeros(output_size)

    def sigmoid(self, x):
        return 1 / (1 + np.exp(-x))

    def forward(self, X):
        self.z1 = np.dot(X, self.W1) + self.b1
        self.a1 = self.sigmoid(self.z1)
        self.z2 = np.dot(self.a1, self.W2) + self.b2
        self.a2 = self.sigmoid(self.z2)
        return self.a2

    def train(self, X, y, epochs=1000, lr=0.1):
        for _ in range(epochs):
            output = self.forward(X)
            error = y - output
            d_output = error * (output * (1 - output))
            d_hidden = np.dot(d_output, self.W2.T) * (self.a1 * (1 - self.a1))
            self.W2 += lr * np.dot(self.a1.T, d_output)
            self.b2 += lr * np.sum(d_output, axis=0)
            self.W1 += lr * np.dot(X.T, d_hidden)
            self.b1 += lr * np.sum(d_hidden, axis=0)
```

- `input_size`：输入层的大小（输入特征的数量）。
- `hidden_size`：隐藏层的大小（隐藏层神经元的数量）。
- `output_size`：输出层的大小（输出神经元的数量，通常为 1 用于二分类）。
- **初始化**：
  - `W1`：输入层到隐藏层的权重矩阵，形状为 `(input_size, hidden_size)`，随机初始化。
  - `b1`：隐藏层的偏置向量，形状为 `(hidden_size,)`，初始化为 0。
  - `W2`：隐藏层到输出层的权重矩阵，形状为 `(hidden_size, output_size)`，随机初始化。
  - `b2`：输出层的偏置向量，形状为 `(output_size,)`，初始化为 0。
  - ![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjdlMzhkNjJkNTg5YmIyMjIzODNmNGY1YjIyN2JmMjdfT2tPOXBxc2xXaDFNWXRDWVRaUm9BWDVmOU51WnFnaDBfVG9rZW46TGlGT2JVZjhhb0V4QTV4c2RqaWM1WVZMbjVnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWRlY2E5NTdjMTBlYjNlZDhkZTE4ZDQzMjNmZWMxYmZfUXhJbTFoRTEwRFRUODdnUjRZeUtBbHNLYlZ4c2dDcUhfVG9rZW46SjVUbmJyMWhzb1NNc3d4ZDhvQ2NtT1pobmVnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

接下来介绍反向传播：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MTU5YzA0ZWZiYjk1ZmZmMTBmMTNlOGRjYjUwNTc0NDBfZjVaN1I1S1F1cHhORkhLdTRvSVpFVUlJa2dGaXlBZEtfVG9rZW46TFQzS2JBNElHb2lOc214TnJmU2M1UTNBbjVlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OWZjMGY1ZTZmZjM1Yjc3NWIwM2E2OTlkNzcxMGEwZTBfNDNBY2x1c0NYaExYNUFqeHFLWVBhSzBuNDBMNTgwN2lfVG9rZW46QnBxQmJxMGxPb0lwb054a25CMmNCQmpoblFmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

对应代码

```Python
error = y - output
d_output = error * (output * (1 - output))
```

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDI3OTZmMWIzZWY1ZTdjYjdiMjc4NGNmOGE0OWViYzNfUElqWFhXMHpJUDljUnhiM29IS3ZVQ25rQXhQcWxOa0lfVG9rZW46U0JMYWJMSndGbzdyZG94ZDR1aGNxZ1F4bjljXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NmVlYmRkYjU4Mjg4MzUxMzI3ZGQ2ODFmODQzNTY0OTVfbWRMc2FPMEwwTzQ4QzRSckF4TVJnUFJMeWFWMlUzelRfVG9rZW46R0I4MWJkUnNpbzhDZW14QkczNmM4RjBObjJYXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDU2ZWM0ZmFiMjBlNDRmNjQ2MDk2NGUxZjgwOGMzMTFfdEVLTk5TR0VRd1BuRE5zaHE1TFRTRVJxaU1WTFJhZXpfVG9rZW46SlZLOWJ5dWwyb3V2eTN4WVd2U2NwMkExbm9mXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

### 2.3 CNN

#### 2.3.1 **CNN 的核心思想**

CNN 的设计灵感来自生物视觉系统，通过局部感受野和权值共享来减少参数数量，同时保留空间信息。它的核心思想包括：

- **局部感受野**：每个神经元只处理输入图像的一小部分区域。
- **权值共享**：使用相同的卷积核在整张图像上滑动，提取特征。
- **层次化特征提取**：通过多层卷积，从低级特征（如边缘）到高级特征（如物体形状）逐步提取。

#### 2.3.2 **CNN 的主要组件**

CNN 通常由以下几个关键组件构成：

##### **(1) 卷积层（Convolutional Layer）**

- **作用**：提取输入数据的局部特征。
- **操作**：使用卷积核（滤波器）在输入数据上滑动，计算点积。
- **输出**：特征图（Feature Map），表示输入数据中某种特征的分布。
- **参数**：
  - 卷积核大小（如 3x3、5x5）
  - 步长（Stride）：卷积核滑动的步长。
  - 填充（Padding）：在输入数据边缘填充像素，控制输出特征图的大小。
  - ![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MTU2M2E1YmRkZTJjZDg5NzkyM2Y3YzRmNTVlMmZjNmJfSGRpTDNMVVlKYndVTXNVcWhKOG5TZ1Z2N05iUEd4T0xfVG9rZW46QWZhVWJUaElnb1BsclZ4N2pnR2N1Z3JCblZnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

##### **(2) 激活函数（Activation Function）**

- **作用**：引入非线性，使网络能够学习复杂的模式。
- 常用激活函数：
  - ReLU（Rectified Linear Unit）：f(x)=max⁡(0,x)
  - Sigmoid、Tanh（较少用于 CNN）

##### **(3) 池化层（Pooling Layer）**

- **作用**：降采样，减少数据维度，同时保留重要特征。
- **常用池化方式**：
  - 最大池化（Max Pooling）：取局部区域的最大值。
  - 平均池化（Average Pooling）：取局部区域的平均值。
- **优点**：
  - 减少计算量。
  - 增强模型的平移不变性。

##### **(4) 全连接层（Fully Connected Layer）**

- **作用**：将提取的特征映射到最终的输出（如分类结果）。
- **特点**：
  - 每个神经元与前一层的所有神经元相连。
  - 通常位于网络的最后几层。

##### **(5) 输出层**

- **作用**：根据任务类型输出结果。
- **常见输出**：
  - 分类任务：Softmax 函数输出概率分布。
  - 回归任务：线性输出。

#### 2.3.3 **CNN 的工作流程**

**输入图像**：将图像数据输入网络。

**卷积操作**：通过卷积核提取局部特征，生成特征图。

**激活函数**：引入非线性，增强模型的表达能力。

**池化操作**：降采样，减少数据维度。

**重复卷积和池化**：通过多层卷积和池化，提取更高层次的特征。

**全连接层**：将特征映射到输出空间。

**输出结果**：根据任务类型输出分类、检测或分割结果。

#### 2.3.4 **CNN 的优势**

- **参数共享**：卷积核在整张图像上共享参数，大大减少了参数量。
- **局部连接**：每个神经元只处理局部区域，降低了计算复杂度。
- **平移不变性**：通过池化操作，CNN 对输入图像的平移具有一定的不变性。
- **层次化特征提取**：从低级到高级特征逐步提取，适合处理图像数据。

#### 2.3.5 **CNN 的经典架构**

以下是一些经典的 CNN 模型：

1. **LeNet-5**：
   1. 最早的 CNN 之一，用于手写数字识别。
   2. 包含卷积层、池化层和全连接层。
2. **AlexNet**：
   1. 2012 年 ImageNet 竞赛冠军。
   2. 引入 ReLU 激活函数和 Dropout 正则化。
3. **VGGNet**：
   1. 使用更深的网络（16-19 层）。
   2. 采用小尺寸卷积核（3x3）。
4. **GoogLeNet**：
   1. 引入 Inception 模块，减少参数量。
5. **ResNet**：
   1. 引入残差连接，解决了深层网络的梯度消失问题。
   2. 可以训练非常深的网络（如 ResNet-152）。

#### 2.3.6 CNN几个概念

##### 2.3.6.1 通道

**通道的基本概念**

- **输入图像的通道**：
  - 对于彩色图像，通常有 3 个通道：红色（R）、绿色（G）和蓝色（B）。
  - 对于灰度图像，只有 1 个通道。
- **卷积层的通道**：
  - 卷积层的输入和输出都有通道。
  - 每个卷积核（滤波器）会生成一个输出通道。
  - 输入通道数由输入数据的通道数决定，输出通道数由卷积核的数量决定。

**输入通道和输出通道的关系**

- **输入通道数**：
  - 由输入数据的通道数决定。例如，彩色图像有 3 个通道，灰度图像有 1 个通道。
- **输出通道数**：
  - 由卷积核的数量决定。例如，使用 2 个卷积核，输出通道数就是 2。
- **卷积核的深度**：
  - 每个卷积核的深度必须与输入通道数相同。例如，输入是 3 通道，卷积核的深度也是 3。

例子：假设我们有一张 **彩色图像**，它的尺寸是 5x5 像素，有 **3 个通道**（红色、绿色、蓝色）。我们用一个卷积层来处理这张图像。

**输入数据**：

- 输入图像的形状：`(1, 3, 5, 5)`
  - `1`：批次大小（1 张图像）。
  - `3`：通道数（红色、绿色、蓝色）。
  - `5, 5`：图像的高度和宽度。

**卷积层**：

- 卷积核的形状：`(2, 3, 3, 3)`
  - `2`：输出通道数（2 个卷积核）。
  - `3`：输入通道数（与输入图像的通道数一致）。
  - `3, 3`：卷积核的高度和宽度。

**输出数据**：

- 输出特征图的形状：`(1, 2, 5, 5)`
  - `1`：批次大小（1 张图像）。
  - `2`：输出通道数（2 个卷积核生成的特征图）。
  - `5, 5`：特征图的高度和宽度。

##### 2.3.6.2 矩阵经过卷积核尺寸变化

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NmYwNjMzMDRiOTMyYTE3MzVjZTc1YTgwODBmOTgyYWVfTlBHVk9KcVpIbnlpa0xpaUFMTzBFU3FydDhmSmVXeXlfVG9rZW46TGtha2JrbUx1b282UDh4WWJzOGNoOEpYbmVlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.3.7 CNN实现mnist数据集例子

```Python
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision
import torchvision.transforms as transforms
from torch.utils.data import DataLoader

# 设置随机种子
torch.manual_seed(42)

# 1. 加载数据集
transform = transforms.Compose([
    transforms.ToTensor(),  # 将图像转换为张量
    transforms.Normalize((0.5,), (0.5,))  # 归一化
])

# 下载并加载训练集
train_dataset = torchvision.datasets.MNIST(root='./data', train=True, download=True, transform=transform)
train_loader = DataLoader(train_dataset, batch_size=64, shuffle=True)

# 下载并加载测试集
test_dataset = torchvision.datasets.MNIST(root='./data', train=False, download=True, transform=transform)
test_loader = DataLoader(test_dataset, batch_size=64, shuffle=False)

# 2. 定义 CNN 模型
class SimpleCNN(nn.Module):
    def __init__(self):
        super(SimpleCNN, self).__init__()
        # 卷积层
        self.conv1 = nn.Conv2d(in_channels=1, out_channels=32, kernel_size=3, stride=1, padding=1)
        self.conv2 = nn.Conv2d(in_channels=32, out_channels=64, kernel_size=3, stride=1, padding=1)
        # 池化层
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)
        # 全连接层
        self.fc1 = nn.Linear(64 * 7 * 7, 128)
        self.fc2 = nn.Linear(128, 10)  # 输出 10 个类别

    def forward(self, x):
        # 卷积 + ReLU + 池化
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        # 展平
        x = x.view(x.size(0), -1)
        # 全连接层
        x = F.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# 实例化模型
model = SimpleCNN()

# 3. 定义损失函数和优化器
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 4. 训练模型
num_epochs = 5
for epoch in range(num_epochs):
    model.train()  # 设置为训练模式
    running_loss = 0.0
    for i, (inputs, labels) in enumerate(train_loader):
        # 清零梯度
        optimizer.zero_grad()
        # 前向传播
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        # 反向传播
        loss.backward()
        optimizer.step()

        running_loss += loss.item()
        if (i + 1) % 100 == 0:
            print(f"Epoch [{epoch + 1}/{num_epochs}], Step [{i + 1}/{len(train_loader)}], Loss: {loss.item():.4f}")

    print(f"Epoch [{epoch + 1}/{num_epochs}], Average Loss: {running_loss / len(train_loader):.4f}")

# 5. 测试模型
model.eval()  # 设置为评估模式
correct = 0
total = 0
with torch.no_grad():
    for inputs, labels in test_loader:
        outputs = model(inputs)
        _, predicted = torch.max(outputs.data, 1)
        total += labels.size(0)
        correct += (predicted == labels).sum().item()

print(f"Test Accuracy: {100 * correct / total:.2f}%")
```

### 2.4 RNN 

#### 2.4.1 Naive RNN

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MGI0ZDA0ZTQ5NGJjNzkzMTAzMjU5ZmZkZmQyMzdhMWFfYmtGNTR6M25QeFVoT0MwbE5rcG1PRlM5VlRXM3FGMllfVG9rZW46RG5hM2I1U21Xb0xBYTl4YXZpbGNxTU0xbmVnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

结构图：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MmYyNGZlMmQwYjRlOTZmYmMwNWI2NWY5M2I4YTg3MWRfQW0wV0hValdOS3g0Zjh3N2ZuamVHblY5UkJtNzFlYk9fVG9rZW46SmtCSGI0czFsb0pQWGh4V0lHcGNPZFFlbkVnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

如何理解隐藏状态？

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NGI0YjVkMWRiOGZiNGM3NTNiZjM2Nzk1NTMxNzg5N2JfRzhWaDBzZG14ZmhtY21uN1RDWmxXY0RhaEd0WWM3RWdfVG9rZW46TnRQQ2JmTUh2b2ZyN1F4ZkRVUWNBN1pRbjI2XzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

看个例子：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NmJiNWZlYzRmZjY5YWIyODA2NjBkYmY2OTllNDBjNzFfNzlLZHlvdkI1akl1ZnBTSmFmWXVvM1Q0WmZidmF1Zk9fVG9rZW46SlBNN2JMMlJqb0llUWV4UHdUYmN2b2F0blRmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YWVhYTcyMTU3ZTcyNTAxMTA5ZGI3Y2RjMmRlZjY2MzdfQjBIcWdlNE5yRXVZajBPbk0zckdON09RajYwRU5ZY2NfVG9rZW46RlFhZ2JKZWZob05RQXN4cEhCSWN2QzkxbldlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MzBhOTk4YzhjNmI1OWU0N2YwNTViNGE1MGE5ZTBmOTlfMDJXdUlNOGRuVXJ6SUxwQ0VBUFZObVhrRms0VEVRa1dfVG9rZW46TEFrS2JadmpFb3FuM3l4UmVIMmNGbXdxbmxmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

再看个例子：给定一个二进制序列（如 `[1, 0, 1, 1]`），RNN 需要预测序列的下一个值。例如，输入 `[1, 0, 1]`，输出应该是 `1`。

```Python
import torch
import torch.nn as nn
import torch.optim as optim

# 定义超参数
input_size = 1      # 输入特征维度（二进制序列，每个元素是 0 或 1）
hidden_size = 16    # 隐藏状态维度
output_size = 1     # 输出维度（预测下一个二进制值）
sequence_length = 4 # 序列长度
num_epochs = 100    # 训练轮数
learning_rate = 0.01

# 生成示例数据
def generate_data(num_samples=1000):
    data = []
    labels = []
    for _ in range(num_samples):
        # 随机生成一个二进制序列
        sequence = torch.randint(0, 2, (sequence_length,)).float()
        # 标签是序列的下一个值
        label = torch.randint(0, 2, (1,)).float()
        data.append(sequence)
        labels.append(label)
    return torch.stack(data), torch.stack(labels)

# 定义 RNN 模型
class SimpleRNN(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super(SimpleRNN, self).__init__()
        self.hidden_size = hidden_size
        self.rnn = nn.RNN(input_size, hidden_size, batch_first=True)
        self.fc = nn.Linear(hidden_size, output_size)

    def forward(self, x):
        # 初始化隐藏状态
        h0 = torch.zeros(1, x.size(0), self.hidden_size)
        # RNN 前向传播
        out, _ = self.rnn(x, h0)
        # 取最后一个时间步的隐藏状态
        out = self.fc(out[:, -1, :])
        return out

# 生成训练数据
X_train, y_train = generate_data(1000)
X_test, y_test = generate_data(200)

# 将数据转换为适合 RNN 的格式 (batch_size, sequence_length, input_size)
X_train = X_train.unsqueeze(-1)
X_test = X_test.unsqueeze(-1)

# 初始化模型、损失函数和优化器
model = SimpleRNN(input_size, hidden_size, output_size)
criterion = nn.MSELoss()  # 使用均方误差损失
optimizer = optim.Adam(model.parameters(), lr=learning_rate)

# 训练模型
for epoch in range(num_epochs):
    # 前向传播
    outputs = model(X_train)
    loss = criterion(outputs, y_train)
    
    # 反向传播和优化
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
    
    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')

# 测试模型
with torch.no_grad():
    test_outputs = model(X_test)
    test_outputs = (test_outputs > 0.5).float()  # 将输出转换为二进制值
    accuracy = (test_outputs == y_test).float().mean()
    print(f'Test Accuracy: {accuracy.item() * 100:.2f}%')

# 示例预测
example_input = torch.tensor([[1, 0, 1, 1]]).float().unsqueeze(-1)
predicted_output = model(example_input)
predicted_value = (predicted_output > 0.5).float()
print(f'Input: {example_input.squeeze().tolist()}, Predicted Next Value: {predicted_value.item()}')
```

#### 2.4.2 LSTM

见https://zhuanlan.zhihu.com/p/42717426

#### 2.4.3 双向RNN

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YjcyODczMGIyNjk0YmM0MGI4ZmE4ODE4YTBhMzY0OTJfajJLbWVrNHFXTkRjQ0VSd0szZW9PU1UxSHk2aDc1U1dfVG9rZW46SmJET2JIaWV5b3JSYVl4ckRjd2N0aERtbmVlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.4.4 多层RNN

**多层 RNN 的核心思想**

多层 RNN 的核心思想是通过堆叠多个 RNN 层，逐层提取序列数据中的特征：

**第一层 RNN**：处理原始输入序列，提取低层次的特征。

**第二层 RNN**：以第一层的输出作为输入，提取更高层次的特征。

**依此类推**：每一层 RNN 都以前一层的输出作为输入，逐步提取更复杂的特征。

**多层 RNN 的结构**

多层 RNN 的结构如下：

**输入层**：接收原始输入序列 x=(x1,x2,…,xT)。

**多个 RNN 层**：

1.  每一层 RNN 都有自己的隐藏状态。

1.  前一层的输出作为后一层的输入。

**输出层**：根据最后一层 RNN 的输出生成最终结果。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJiNGNkZTdjOWY5ZmYxZDAwNTBjOTg5NTZjYmVjMzNfRHpmUncwMm4wT2lvQVJqb000cHlCTXdhODBwNEV3NWFfVG9rZW46UXlJcmJnVGRPb0tBUHh4U0hMQWNTMEEzbnJlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODc4NTdiY2RlZDYwNTQ1YWYzNTFlZmNhMTA0MzJiMGVfSHZsaFRpdWlzM1lRV1BYNG1tekhXUnplMWRzYmVYMWJfVG9rZW46RXc5ZWJLTXJQb0JXV2p4RWZsUWNFQmFwbmJnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

```Python
import torch
import torch.nn as nn

# 定义多层 RNN 模型
class MultiLayerRNN(nn.Module):
    def __init__(self, input_size, hidden_size, output_size, num_layers=2):
        super(MultiLayerRNN, self).__init__()
        self.hidden_size = hidden_size
        self.num_layers = num_layers
        # 多层 RNN
        self.rnn = nn.RNN(input_size, hidden_size, num_layers, batch_first=True)
        # 全连接层
        self.fc = nn.Linear(hidden_size, output_size)

    def forward(self, x):
        # 初始化隐藏状态
        h0 = torch.zeros(self.num_layers, x.size(0), self.hidden_size)
        # RNN 前向传播
        out, _ = self.rnn(x, h0)
        # 使用最后一个时间步的隐藏状态生成输出
        out = self.fc(out[:, -1, :])
        return out

# 示例参数
input_size = 10
hidden_size = 20
output_size = 1
num_layers = 3

# 创建模型
model = MultiLayerRNN(input_size, hidden_size, output_size, num_layers)

# 示例输入
x = torch.randn(3, 5, 10)  # (batch_size, seq_len, input_size)

# 前向传播
output = model(x)
print("Output shape:", output.shape)  # 输出: (batch_size, output_size)
```

#### 2.4.5 RNN总结

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmQyOGVmY2IyYmZiMGFiNzI3MzgyNTgwYWM1NTZlMjdfaVRSTngzb3lVcXJ3RTlxemFlQXJyeUNrbjJmbWtuTWFfVG9rZW46UkNWMGJxU29lbzNwTWJ4OXdpbGN2d3BNbk9kXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 3、NLP

以下内容参考（https://transformers.run/c1/nlp/）

### 3.1 自然语言处理发展史

自然语言处理的发展大致上可以分为两个阶段：

**第一阶段：不懂语法怎么理解语言？**

20 世纪 50 年代到 70 年代，人们对自然语言处理的认识都局限在人类学习语言的方式上，用了二十多年时间苦苦探寻让计算机理解语言的方法，最终却一无所获。

当时的学术界普遍认为，要让计算机处理自然语言必须先让其理解语言，因此分析语句和获取语义成为首要任务，而这主要依靠语言学家人工总结文法规则来实现。特别是 20 世纪 60 年代，基于乔姆斯基形式语言（Chomsky Formal languages）的编译器取得了很大进展，更加鼓舞了研究者通过概括语法规则来处理自然语言的信心。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=M2YxMzNkOGU5ODEyYzlkZTZhYTIyNDg0NzdmNzJmNzlfazhlSGh0T04xTElvQ2NWWkRIcGxBcE1wWkNJcDFuUkZfVG9rZW46U3Mxd2JvVjJUb0FsN1d4U0xDa2NocTdPbnhjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

但是与规范严谨的程序语言不同，自然语言复杂又灵活，是一种上下文有关文法（Context-Sensitive Grammars，CSGs），因此仅靠人工编写文法规则根本无法覆盖，而且随着编写的规则数量越来越多、形式越来越复杂，规则与规则之间还可能会存在矛盾。因此这一阶段自然语言处理的研究可以说进入了误区。

**第二阶段：只要看的足够多，就能处理语言**

正如人类是通过空气动力学而不是简单模仿鸟类造出了飞机，计算机处理自然语言也未必需要理解语言。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NTFmNjFhYmE3OGI3MzdkZmFjODgzY2IyNWI1ZDNmNDRfeEtnRVNmaHhOdTliNkhoNjU3Mkg4cUx1N3VsalhCbHhfVG9rZW46SmVhVWJqbUNab2FIOVh4WnV5RmNRUFJIbmFkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

20 世纪 70 年代，随着统计语言学的提出，基于数学模型和统计方法的自然语言处理方法开始兴起。当时的代表性方法是“通信系统加隐马尔可夫模型”，其输入和输出都是一维且保持原有次序的符号序列，可以处理语音识别、词性分析等任务，但是这种方法在面对输出为二维树形结构的句法分析以及符号次序有很大变化的机器翻译等任务时就束手无策了。

20 世纪 80 年代以来，随着硬件计算能力的提高以及海量互联网数据的出现，越来越多的统计机器学习方法被应用到自然语言处理领域，例如一些研究者引入基于有向图的统计模型来处理复杂的句法分析任务。2005 年 Google 公司基于统计方法的翻译系统更是全面超过了基于规则的 SysTran 系统。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NTc3N2EyNGI3MWIyMmM2N2JhYjNmYTA2ODI1ODJkOTZfOEg5Z3phandtb2R2NHZWU21NVEFPbm1CQWlrOUczamZfVG9rZW46QTlwNmJscVBzb2ttOHp4cW4xbGNrSzVIbmJoXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

2006 年，随着辛顿（Hinton）证明深度信念网络（Deep Belief Networks，DBN）可以通过逐层预训练策略有效地进行训练，基于神经网络和反向传播算法（Back Propagation）的深度学习方法开始兴起。许多之前由于缺乏数据、计算能力以及有效优化方法而被忽视的神经网络模型得到了复兴。例如 1997 年就已提出的长短时记忆网络（Long Short Term Memory，LSTM）模型在重新被启用后在许多任务上大放异彩

```LaTeX
即使在 Transformer 模型几乎“一统江湖”的今天，LSTM 模型依然占有一席之地。2024 年 5 月 8 日，LSTM 提出者和奠基者 Sepp Hochreiter 公布了 LSTM 模型的改良版本——xLSTM，在性能和扩展方面都得到了显著提升。论文的所属机构中还出现了一家叫做 NXAI 的公司，Sepp Hochreiter 表示：“借助 xLSTM，我们缩小了与现有最先进大语言模型的差距。借助 NXAI，我们已开始构建欧洲自己的大语言模型。”
```

随着越来越多研究者将注意力转向深度学习方法，诸如卷积神经网络（Convolutional Neural Networks，CNN）等模型被广泛地应用到各种自然语言处理任务中。2017 年，Google 公司提出了 Attention 注意力模型，论文中提出的 Transformer 结构更是引领了后续神经网络语言模型的发展。

得益于抛弃了让计算机简单模仿人类的思路，这一阶段自然语言处理研究出现了蓬勃发展。今天可以说已经没有人再会质疑统计方法在自然语言处理上的可行性。

### 3.2 统计语言模型发展史

#### 3.2.1 统计语言模型

20 世纪 70 年代之前，研究者尝试从文字序列是否合乎文法、含义是否正确的角度来建立语言模型。最终，随着人工编写出的规则数量越来越多、形式越来越复杂，对语言模型的研究陷入瓶颈。直到 20 世纪 70 年代中期，IBM 实验室的贾里尼克（Jelinek）为了研究语音识别问题换了一个思路，用一个简单的统计模型就解决了这个问题。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NWRlZWMwMWQ4YWZmYzVlOWJkYzk2ZWY1ZGFhZDYwODdfczBaSG9wVTFEVXYydnJ0SmhZY1FHYzB5Tlhyd2h3YVdfVG9rZW46UmQxU2JoUFIxbzllNzR4TlRxcmNnSWJjbnBjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 3.2.2 NNLM模型

NNLM 的核心思想是通过神经网络来建模语言的概率分布，即给定前 n−1个词，预测第 n个词的概率。与传统基于统计的 n-gram 语言模型不同，NNLM 能够捕捉词与词之间的分布式表示（distributed representation），从而更好地处理语言的复杂性和长距离依赖关系。

**NNLM 的模型结构**

NNLM 的模型结构主要包括以下几个部分：

**(1) 输入层**

输入是前 n−1个词的 one-hot 向量。

假设词汇表大小为 V，则每个词的 one-hot 向量维度为 V。

**(2) 词嵌入层（Embedding Layer）**

将 one-hot 向量映射到一个低维的稠密向量（词向量）。

假设词向量的维度为 D，则词嵌入矩阵 C的形状为 V×D。

**(3) 隐藏层**

将词向量拼接成一个长向量，输入到一个全连接层（隐藏层）。

假设隐藏层的维度为 H，则隐藏层的权重矩阵 W*W* 的形状为 ((n−1)×D)×H，偏置向量 b 的形状为 H。

**(4) 输出层**

隐藏层的输出通过一个全连接层映射到词汇表大小的向量。

输出层的权重矩阵 U 的形状为 H×V，偏置向量 d的形状为 V。

使用 softmax 函数将输出转换为概率分布。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=N2VmYmM4ZTA1NzkzOWIwZjEwOWFiNWVkYzFiYWJjMTlfQ0Z1VFFuVm5Ielg1SXlwd1dLY2FuRGZTS1NZNzhqWlVfVG9rZW46TGRYa2IxYWxEb3pRSnl4enJoSmNxWlAzbmtjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MWE5ZGYyYjdkMTdiMjY0MzlkOTk0NTdmOWM4MDVhMjRfWHk2VGdyRG03a2NUWkJaSjV1dWpyNW05VWxDWTJpWFBfVG9rZW46V0JOamJZanRib3Y5UHR4anM1a2NtU3FYbnNlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

**词嵌入层的解释：**

1、**词嵌入层的作用**

词嵌入层的主要作用是将高维的 one-hot 向量映射为低维的稠密向量。具体来说：

**输入**：一个词语的 one-hot 向量，维度为词汇表大小 V*V*。

**输出**：一个低维的稠密向量，维度为 D（通常 D≪V）。

通过词嵌入层，模型能够学习到词语的分布式表示（distributed representation），从而捕捉词语之间的语义关系。

2、**词嵌入层的实现**

词嵌入层通常通过一个**嵌入矩阵**（Embedding Matrix）来实现。假设词汇表大小为 V，词向量维度为 D，则嵌入矩阵 C 的形状为 V×D。

**(1) 输入：one-hot 向量**

假设词汇表为 `["我", "爱", "学习", "NLP"]`，对应的索引为：

"我": 0

"爱": 1

"学习": 2

"NLP": 3

词语 "爱" 的 one-hot 向量为：

[0, 1, 0, 0]

**(2) 嵌入矩阵**

假设词向量维度 D=2，嵌入矩阵 C*C*可能如下：

C

**(3) 映射过程**

将 one-hot 向量与嵌入矩阵相乘，得到词向量。例如，词语 "爱" 的 one-hot 向量为 `[0, 1, 0, 0]`，与嵌入矩阵 C 相乘：

词向量=[0,1,0,0]⋅C=[0.3,0.4]

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YzVmMTM0ZGU1MjEzNDk1Mzc5ZDhmMTE3NGJlOWNlZDBfd0dSb2diemZQN0owRFhvMWxuUWJSSkxJUFdxaWRrZ3lfVG9rZW46VjFFcWI1OERSbzg0eEd4ZTNzZGNpVE5TbnhjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

看个例子：

```Python
import torch
import torch.nn as nn
import torch.optim as optim

# 定义 NNLM 模型
class NNLM(nn.Module):
    def __init__(self, vocab_size, embedding_dim, hidden_dim, context_size):
        super(NNLM, self).__init__()
        self.embeddings = nn.Embedding(vocab_size, embedding_dim)
        self.linear1 = nn.Linear(context_size * embedding_dim, hidden_dim)
        self.linear2 = nn.Linear(hidden_dim, vocab_size)

    def forward(self, inputs):
        # 将输入索引映射为词向量
        embeds = self.embeddings(inputs).view((1, -1))  # 拼接词向量
        # 隐藏层
        out = torch.tanh(self.linear1(embeds))
        # 输出层
        out = self.linear2(out)
        # 使用 log_softmax 计算对数概率
        log_probs = torch.log_softmax(out, dim=1)
        return log_probs

# 示例参数
vocab_size = 4  # 词汇表大小
embedding_dim = 2  # 词向量维度
hidden_dim = 3  # 隐藏层维度
context_size = 2  # 上下文窗口大小

# 创建模型
model = NNLM(vocab_size, embedding_dim, hidden_dim, context_size)

# 定义损失函数和优化器
criterion = nn.NLLLoss()  # 负对数似然损失
optimizer = optim.SGD(model.parameters(), lr=0.1)

# 示例输入
inputs = torch.tensor([0, 1])  # 输入 "我" 和 "爱" 的索引
target = torch.tensor([2])     # 目标词 "学习" 的索引

# 训练模型
for epoch in range(100):
    # 前向传播
    log_probs = model(inputs)
    loss = criterion(log_probs, target)
    
    # 反向传播和优化
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
    
    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/100], Loss: {loss.item():.4f}')

# 测试模型
with torch.no_grad():
    test_input = torch.tensor([0, 1])  # 输入 "我" 和 "爱"
    log_probs = model(test_input)
    predicted_index = torch.argmax(log_probs, dim=1).item()
    print(f"输入: ['我', '爱'], 预测的下一个词索引: {predicted_index}")
```

#### 3.2.3 Word2Vec 模型

真正将神经网络语言模型发扬光大的是 2013 年 Google 公司提出的 Word2Vec 模型。Word2Vec 模型提供的词向量在很长一段时间里都是自然语言处理方法的标配，即使是后来出现的 Glove 模型也难掩它的光芒。

Word2Vec 的模型结构和 NNLM 基本一致，只是训练方法有所不同，分为 CBOW (Continuous Bag-of-Words) 和 Skip-gram 两种，如图 1-7 所示。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzE5YzFjZWM3OWVmMjZkZGU1NDZkNmJlMzMwOTJmMWFfUUtwMTQ1aktQc09tQ0I4b1ppYUNOS0JicjltMklQdUpfVG9rZW46QW1obGJlT2tHb0dMeE54MjdOc2NZc0o0bm5mXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzNjMzVlOTM0MzNmNzg2YTIwMzI2ZDA2OGJhNGRmMjJfOUROYnIxcnN4dW1SUXJQMzgwU2hoV3J2S29SRENkYVlfVG9rZW46TzBENGJJNHBCb3Z4RUd4bjFYVWM5SE5ObjRiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

可以看到，与严格按照统计语言模型结构设计的 NNLM 模型不同，Word2Vec 模型在结构上更加自由，训练目标也更多地是为获得词向量服务。特别是同时通过上文和下文来预测当前词语的 CBOW 训练方法打破了语言模型“只通过上文来预测当前词”的固定思维，为后续一系列神经网络语言模型的发展奠定了基础。

然而，有一片乌云一直笼罩在 Word2Vec 模型的上空——多义词问题。一词多义是语言灵活性和高效性的体现，但是 Word2Vec 模型却无法处理多义词，一个词语无论表达何种语义，Word2Vec 模型都只能提供相同的词向量，即将多义词编码到了完全相同的参数空间。实际上在 20 世纪 90 年代初，雅让斯基（Yarowsky）就给出了一个简洁有效的解决方案——运用词语之间的互信息（Mutual Information）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YzRkZTI5ZTNlOTljMTJmMzY4MGVmMzdiYjRhZmQ2NjdfSHhKSnBpcTBiQmc2VXdwQU9kdElVdFdMTGxhRFpiZmtfVG9rZW46RzZ2cmJiVG5pb1BCSnh4d0pna2M4WklJbk5mXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

具体来说，对于多义词，可以使用文本中与其同时出现的互信息最大的词语集合来表示不同的语义。例如对于“苹果”，当表示水果时，周围出现的一般就是“超市”、“香蕉”等词语；而表示“苹果公司”时，周围出现的一般就是“手机”、“平板”等词语，如图 1-9 所示。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmMyNDcxNTc3M2E2MTY0MmE4Njg1OWZkNTRlOGZjYWFfajlFbWJ6TFJPUTBqWWUxRGNSYWltdXJ6OFQ0NW5YeFZfVG9rZW46WE9KQ2JSNTBtb2RMNWp4VTNBd2MyQnIxbkZnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 3.2.4 ELMO模型

1、**ELMo 的核心思想**

ELMo 的核心思想是：**词语的含义不仅取决于其本身，还取决于其上下文**。传统的词嵌入模型（如 Word2Vec）为每个词生成一个固定的向量表示，而 ELMo 通过双向语言模型生成动态的词向量，能够更好地捕捉词语的多义性和上下文依赖关系。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjZjMDU1M2Y4NWQwYTdkMmQ0NDMyNjMzZGZiZmI4Y2FfbW9kZWpxUjFaSHlwUmQ5QUdDaG5BNGVZMUh3T3RXcklfVG9rZW46T1lsYmJoYkxRb25uS2N4V1lFcmNrMFZvbllkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OWVjNjYxNzE4ZDM2NWM3NjA0YjQzMmQ4MGUyMmJlZjlfcVB3d1lCdzgxakJRakU2bUk5NEcxcXIwV0MzTndKdFdfVG9rZW46UHZ0Z2J5U1Q3b2pCRll4VEUwSGN1VEs2bndiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjU1Y2QzY2Y4ZDMxYjY2MDY3ZThiYTQyNTQxZmUwZTFfVDZnRTd2NU5ibFRNUnpkSnlJN1F4U0VoMXlrV0Z5MFhfVG9rZW46WXZvOWJoYkhVbzc1Yld4WEE4eWNIS0FCblk1XzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

但是 ELMo 模型存在两个缺陷：首先它使用 LSTM 模型作为编码器，而不是当时已经提出的编码能力更强的 Transformer 模型；其次 ELMo 模型直接通过拼接来融合双向抽取特征的做法也略显粗糙。

不久之后，将 ELMo 模型中的 LSTM 更换为 Transformer 的 GPT 模型就出现了。但是 GPT 模型再次追随了 NNLM 的脚步，只通过词语的上文进行预测，这在很大程度上限制了模型的应用场景。例如对于文本分类、阅读理解等任务，如果不把词语的下文信息也嵌入到词向量中就会白白丢掉很多信息。

#### 3.2.5 seq2seq和attention详解

##### **seq2seq模型** 

是一种用于处理序列到序列映射的神经网络模型，最初由 Google 在 2014 年提出，主要用于机器翻译任务。它的核心思想是将输入序列映射到一个固定长度的向量（上下文向量），然后将该向量解码为输出序列。Seq2Seq 模型在自然语言处理（NLP）领域有着广泛的应用，如机器翻译、文本摘要、对话系统等。

**1、Seq2Seq 的核心思想**

Seq2Seq 模型的核心思想是：**将输入序列编码为一个固定长度的上下文向量，然后通过解码器生成输出序列**。它的主要特点是：

输入和输出都是序列。

输入序列和输出序列的长度可以不同。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODAwMWQxYjYwY2I2ZTc1ZDFkYjk3ZDNkZTkxMWJjNzZfQjRRUXk3WlI3cFJKeTlZUjdLR0wxRVladkdZdjA2aW9fVG9rZW46SmVmTGJOT0Vzb0l3alB4OGlsM2NYcWVqbjlkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NmM1OGI5YjI0NzJjNGJkMGJlMGE0ZmMzYmM5NTcyNDFfR09nSFZ6eEtHcFVqRkg5VmdYZU5wSnpackZ2RmtZTFJfVG9rZW46VzlVZWJoWGVjb05UbUx4M3JGQ2N6Z0RublplXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

看图：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MmRkNDBmMTNkNjc2MjVmMjFmZGE5NDk2MzI4M2Y0ZGVfamZwQTdETE1BaHlKS1NMNlA5NnRzMUoyNWlaeTl2WHhfVG9rZW46RUNad2JYVEppb0UwazN4S29iWWNxZm9TblpkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

再看个例子：

假设我们有一个非常小的词汇表和简单的句子，目标是训练一个 Seq2Seq 模型来实现**数字反转**任务。例如，输入序列是 `[1, 2, 3]`，输出序列是 `[3, 2, 1]`。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NTI1YTkzZWQ4N2I4Mjk1OGQ1N2JiYjZjZTYyMDA4MGRfYUJURHkyb2tZelBZSm9yYmE4REJ3bGxxNVNvek9BV0RfVG9rZW46TzU4TGJ3aVEzb0lsVUd4U08zbWN2clVHbjc5XzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDgwMjUwYmNmNjRkMGY0NDkyYzc2MDVmYjkwNzg3NTdfWUs2NEt3Y1JyQTF0Q1AxbWZ6bmJjS0RnaHR5NzBnbmlfVG9rZW46TldKRmJFQm5zb0owM2Z4bnNpZGNLR0hJbmFnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzEwMTQ2YzI3ODgyZWJkNTdhMmE5MmFkN2M5MzVlNGRfeXVxSng1U1pXcjVVNnlVbHJDWXRSREVPejR5aGloZm1fVG9rZW46TnhwM2JTYlVsbzd3RjR4Sm5GVGNtQ0tZbkxkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzMzMTFlZTA4NDdjNjJkMWYwNzU5YThjYjk4MzFjNmRfYkFyNzQ3alkzUko5emsyenJnN2Y5b3FXbWpDb2l2aGJfVG9rZW46WVdJWWJrbnFVb3lPdnN4Q21oN2N2YUJjbmpmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

以下是使用 PyTorch 实现的简单 Seq2Seq 模型示例：

```Python
import torch
import torch.nn as nn

# 定义 Seq2Seq 模型
class Seq2Seq(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super(Seq2Seq, self).__init__()
        self.hidden_size = hidden_size

        # 编码器
        self.encoder = nn.GRU(input_size, hidden_size, batch_first=True)

        # 解码器
        self.decoder = nn.GRU(hidden_size, hidden_size, batch_first=True)

        # 输出层
        self.fc = nn.Linear(hidden_size, output_size)

    def forward(self, src, trg):
        # 编码器
        _, hidden = self.encoder(src)

        # 解码器
        trg_len = trg.shape[1]
        batch_size = trg.shape[0]
        outputs = torch.zeros(batch_size, trg_len, self.fc.out_features)

        # 初始输入（开始符号 <SOS>）
        input = trg[:, 0, :].unsqueeze(1)

        for t in range(trg_len):
            output, hidden = self.decoder(input, hidden)
            output = self.fc(output.squeeze(1))
            outputs[:, t, :] = output

            # 下一个输入是当前输出
            input = output.unsqueeze(1)

        return outputs

# 示例参数
input_size = 5  # 词汇表大小
hidden_size = 10  # 隐藏层大小
output_size = 5  # 词汇表大小
batch_size = 1  # 批量大小

# 创建模型
model = Seq2Seq(input_size, hidden_size, output_size)

# 定义损失函数和优化器
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)

# 示例输入和输出
src = torch.tensor([[2, 3, 4]])  # 输入序列 [1, 2, 3]
trg = torch.tensor([[4, 3, 2]])  # 输出序列 [3, 2, 1]

# 将输入和输出转换为 one-hot 向量
src_onehot = F.one_hot(src, num_classes=input_size).float()
trg_onehot = F.one_hot(trg, num_classes=output_size).float()

# 训练模型
for epoch in range(100):
    # 前向传播
    outputs = model(src_onehot, trg_onehot)

    # 计算损失
    loss = criterion(outputs.view(-1, output_size), trg.view(-1))

    # 反向传播和优化
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/100], Loss: {loss.item():.4f}')

# 测试模型
with torch.no_grad():
    test_input = torch.tensor([[2, 3, 4]])  # 输入序列 [1, 2, 3]
    test_input_onehot = F.one_hot(test_input, num_classes=input_size).float()
    outputs = model(test_input_onehot, trg_onehot)
    predicted = torch.argmax(outputs, dim=2)
    print("输入序列:", src.tolist())
    print("预测输出:", predicted.tolist())
```

**Seq2Seq 的局限性**

**上下文向量瓶颈**：

1.  编码器需要将整个输入序列压缩为一个固定长度的向量，可能导致信息丢失。

**长序列问题**：

1.  对于长序列，RNN 难以捕捉长距离依赖关系。

##### **Attention 机制**

为了解决 Seq2Seq 模型的局限性，Attention 机制被引入。它的核心思想是：**在解码时，动态地关注输入序列的不同部分**，而不是依赖于单一的上下文向量。

看图更好理解

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NTVlZWVkNjczMzllZmU2Y2FlYzYzM2E0YWZhMDk0ODVfNkFLdllidmVZNWhiQnFmcTZOeWpubWVMNmpHYUVZYzBfVG9rZW46S0ZkcWJ6SDJLb1RoU214WlFtU2NmU2NRbjhiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

**Attention 的核心思想**

**动态权重分配**：

1.  对于每个输出元素，模型会计算输入序列中每个元素的权重。

1.  权重越大，表示该输入元素对当前输出的贡献越大。

**上下文向量生成**：

1.  根据权重对输入序列进行加权求和，生成上下文向量。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmM2N2FiYmIxMWE1ZDBmYTNmNmE2YmE3NWRmZmY1MDhfbzRIajM3VUVqa2EwaFJORG9qcGhUTERBZWJlWGRLZHVfVG9rZW46UmNiUGJDMHF4b2ZzdHF4ekE0c2NkSERKbmhkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 4、transformer基础知识

transformer是一种基于 **Attention 机制** 的深度学习模型，由 Vaswani 等人在 2017 年提出。它在自然语言处理（NLP）领域取得了巨大成功，广泛应用于机器翻译、文本生成、语音识别等任务。Transformer 的核心思想是完全基于 Attention 机制，摒弃了传统的循环神经网络（RNN）和卷积神经网络（CNN），从而实现了更高的并行性和更好的性能。

**Transformer 的核心组件**

Transformer 模型由以下几个核心组件组成：

**输入嵌入（Input Embedding）**

**位置编码（Positional Encoding）**

**多头自注意力机制（Multi-Head Self-Attention）**

**前馈神经网络（Feed-Forward Network）**

**残差连接和层归一化（Residual Connection & Layer Normalization）**

**编码器-解码器架构（Encoder-Decoder Architecture）**

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NjdmMDE1MWVmNGE5NTc2NGUwYTM3OGRlYWJkZTE3MjdfZGdUUG9mTnk4Z0VZcTg5SkhTTkhmT0p3TUtsRmhLOFBfVG9rZW46Qnd6a2JwN0xCb1U3a3N4ck9JVmNmeURRbldnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

### 4.1 transformer结构

### 4.1.1 Word **Embedding + Positional Encoding**

我们输入数据 `X` 维度为`[batch size, sequence length]`的数据，比如`我们为什么工作`。

`batch size` 就是 `batch` 的大小，这里只有一句话，所以 `batch size` 为 `1`，`sequence length` 是句子的长度，一共 `7` 个字，所以输入的数据维度是 `[1, 7]`。

我们不能直接将这句话输入到**编码器**中，因为 `Tranformer` 不认识，我们需要先进行**字嵌入**，即得到图中的 𝑋embedding 。简单点说，就是文字->字向量的转换，这种转换是将文字转换为计算机认识的数学表示，用到的方法就是 `Word2Vec`。得到的 𝑋embedding  的维度是 `[batch size, sequence length, embedding dimension]`，`embedding dimension` 的大小由 `Word2Vec` 算法决定，`Tranformer` 采用 `512` 长度的字向量。所以 𝑋embedding  的维度是 `[1, 7, 512]`。至此，输入的`我们为什么工作`，可以用一个矩阵来简化表示。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NjhiNzAyOTExYmNiOGMzOTBlMGZlYTcyNmZlZGNiZjVfQTI2Y0VwRld5VEpvdFM5TmVqTjVaOEw0anEzN0E5R09fVG9rZW46T09YTGIyODcyb1NJdGZ4TUVYaWNCWU1IbjhnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

我们知道，文字的先后顺序，很重要。

比如`吃饭没`、`没吃饭`、`没饭吃`、`饭吃没`、`饭没吃`，同样三个字，顺序颠倒，所表达的含义就不同了。

文字的位置信息很重要，`Tranformer` 没有类似 `RNN` 的循环结构，没有捕捉顺序序列的能力。

为了保留这种位置信息交给 `Tranformer` 学习，我们需要用到**位置嵌入**。

加入位置信息的方式非常多，最简单的可以是直接将绝对坐标 `0,1,2` 编码。

`Tranformer` 采用的是 `sin-cos` 规则，使用了 `sin` 和 `cos` 函数的线性变换来提供给模型位置信息：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzg0MWVkNWE2OTQxYzVlY2I0NjdlOGJlNzdkMzEwYmJfeW1Ca2hORGJ6S0k4cjdHWG1rT3Q2Y3FJY2ZONm1GYTFfVG9rZW46UUFMbWJzWTQ5b1Jhak54Mk1EVmNibHNQblJkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NWU0YWU1Njk4NDAyMmI4MzE3ZGZiMDQ3MmU1NzRkZjVfZ3pId2RvWXdFNmFSY2FVN0ZwMjJkYjFrdnhkTEU3QWJfVG9rZW46UWlUcWJNT0tUb2JPdzd4UURnUmNPV2RDbkdkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

### 4.1.2 **Multi-Head Self-Attention**

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YWE4ZjI3ZDgzYzVkNDgyNmM0MDkxNmI0ZjIxZjIzYmRfdGIwR3EwOGFMQ1RteENmVWZLWjJLbkhINVlTaEVTWWRfVG9rZW46SkhTQWJvQ3NHb3M2Nmd4SFQ1dWNGN2Jobk1nXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NGI3ZTMwODZiYWQ2MmE4MDhkNjA2NzYyYzgyY2RjYjJfcU54SEM1WkxVZWNKNldJYWJ5Y0J5WFFZVDJuNmJmT0JfVG9rZW46Wm9CVWJoZENjb1VPUWh4ZzZXSWNPZ2VMbmllXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODE4ZDA2YzY2NDZmYzkyN2JlZmRhNDhhOGJkYTM0YjFfTUpqTGlVd1A3bTNqS0ZSUnkxNElGRjg0T0N4M045WUpfVG9rZW46WEg0eWJYNUJzb01ya3d4bkF0QmNxRnRkbnAzXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

上面多头注意力部分讲的不是很清楚，我们一起看个例子

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=Njg3N2NlYzJkZDE2OTM0ZmJiM2Y4OWJhOTBlMjdkZGZfUjluSGIycEpPakR4UzA1N0ZyV2gxSEZxRUp6UjlrNmpfVG9rZW46UzVyamJLS21Yb2Q4ZFV4MzhLc2NZQm9ZbjBlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NWY0NDkzOGFjZTRmZDkzNWVmY2I3ZDhlYmRlNzQ4NzFfc2hjSGdQTklJQWVMN05SNDVLbXRYaXBVbEw2a1dXWVVfVG9rZW46TUJ4UmJxUWRSb0s4VGd4Y09NNGNGZUNWbjNiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

Numpy 实现multi-head attention

```Python
import numpy as np

def softmax(x):
    # 减去最大值，防止值溢出
    exp_x = np.exp(x - np.max(x, axis=-1, keepdims=True))
    return exp_x / np.sum(exp_x, axis=-1, keepdims=True)

def scaled_dot_product_attention(Q, K, V):
    d_k = Q.shape[-1]
    scores = np.matmul(Q, K.transpose(0, 2, 1)) / np.sqrt(d_k)  # 计算注意力分数
    attention_weights = softmax(scores)  # softmax归一化
    output = np.matmul(attention_weights, V)  # 加权求和
    return output

def multi_head_attention(X, W_Q, W_K, W_V, W_O, num_heads):
    batch_size, seq_len, d_model = X.shape
    d_k = d_model // num_heads  # 每个头的维度

    # 线性变换得到 Q, K, V
    Q = np.matmul(X, W_Q)  # [batch_size, seq_len, d_model]
    K = np.matmul(X, W_K)  # [batch_size, seq_len, d_model]
    V = np.matmul(X, W_V)  # [batch_size, seq_len, d_model]

    # 将 Q, K, V 分成多个头
    Q = Q.reshape(batch_size, seq_len, num_heads, d_k).transpose(0, 2, 1, 3)  # [batch_size, num_heads, seq_len, d_k]
    K = K.reshape(batch_size, seq_len, num_heads, d_k).transpose(0, 2, 1, 3)  # [batch_size, num_heads, seq_len, d_k]
    V = V.reshape(batch_size, seq_len, num_heads, d_k).transpose(0, 2, 1, 3)  # [batch_size, num_heads, seq_len, d_k]

    # 对每个头计算注意力
    attention_outputs = []
    for i in range(num_heads):
        head_output = scaled_dot_product_attention(Q[:, i], K[:, i], V[:, i])  # 计算单个头的注意力
        attention_outputs.append(head_output)
    attention_outputs = np.stack(attention_outputs, axis=1)  # [batch_size, num_heads, seq_len, d_k]

    # 拼接所有头的输出
    attention_outputs = attention_outputs.transpose(0, 2, 1, 3).reshape(batch_size, seq_len, d_model)  # [batch_size, seq_len, d_model]

    # 线性变换得到最终输出
    output = np.matmul(attention_outputs, W_O)  # [batch_size, seq_len, d_model]
    return output

# 示例数据
batch_size = 1
seq_len = 2
d_model = 4
num_heads = 2

# 输入序列 X
X = np.array([[[1, 2, 3, 4], [4, 3, 2, 1]]])  # [batch_size, seq_len, d_model]

# 权重矩阵
W_Q = np.random.randn(d_model, d_model)
W_K = np.random.randn(d_model, d_model)
W_V = np.random.randn(d_model, d_model)
W_O = np.random.randn(d_model, d_model)

# 计算多头注意力
output = multi_head_attention(X, W_Q, W_K, W_V, W_O, num_heads)
print("输入 X:\n", X)
print("多头注意力输出:\n", output)
```

### 4.1.3 Feed-Forward 层

Feed-Forward 层是 Transformer 中的一个重要组件，位于自注意力机制（Self-Attention）之后。它的作用是对自注意力机制输出的特征进行非线性变换，从而增强模型的表达能力。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmZlZjg4MjQ3MmRlZDc4NmQ5YmUxZTRhOWU0ZmY2MTFfamdnZVh0T1RsZHJkcExBTFUzMFd3MkRJQlowV1g4SW5fVG9rZW46Ukg4UGJwTmkzb280dW54aUxFR2NNWVVpblRiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

### 4.1.4 残差链接和层归一化

残差连接（Residual Connection）

1.1 残差连接的作用

残差连接是一种深度学习中的技术，最早在 ResNet 中提出。它的作用是解决深层网络中的梯度消失问题，并帮助模型更好地训练。

在 Transformer 中，残差连接被广泛应用在以下两个地方：

**自注意力层之后**：将自注意力层的输出与输入相加。

**前馈神经网络层之后**：将前馈神经网络层的输出与输入相加。

1.2 残差连接的公式

残差连接的公式非常简单：

Output=Layer(x)+x

其中：

x是输入。

Layer(x) 是某一层的输出（例如自注意力层或前馈神经网络层）。

1.3 残差连接的意义

**梯度传播**：残差连接可以让梯度直接通过加法操作回传，缓解梯度消失问题。

**特征复用**：模型可以更容易地学习到输入和输出之间的差异，而不是完全重新学习输入。

归一化层（Layer Normalization）

2.1 归一化层的作用

归一化层的作用是对输入进行标准化处理，使得每一层的输入分布更加稳定，从而加速模型训练并提高模型的泛化能力。

在 Transformer 中，归一化层通常用在以下两个地方：

**自注意力层之后**：对自注意力层的输出进行归一化。

**前馈神经网络层之后**：对前馈神经网络层的输出进行归一化。

2.2 归一化层的公式

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NjMxNDAyZDhjYzliZTFjMDU5NjFjOWRlYTIzMDQ2ZmFfTDZUQXJCTElPd2owaWs5UTZJV2xydFFCdGtpSU9mT09fVG9rZW46QjJJOGJOaTF3b1dSQWR4YzI3QWNVemkwbkJoXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

2.3 归一化层的意义

**稳定训练**：归一化层可以使得每一层的输入分布更加稳定，减少内部协变量偏移（Internal Covariate Shift）。

**加速收敛**：归一化层可以加速模型的收敛速度。

### 4.1.5 pytorch实现transformer

```Python
import torch
import torch.nn as nn
import torch.nn.functional as F
import math
class PositionalEncoding(nn.Module):
    def __init__(self, d_model, max_len=5000):
        super(PositionalEncoding, self).__init__()
        pe = torch.zeros(max_len, d_model)
        position = torch.arange(0, max_len, dtype=torch.float).unsqueeze(1)
        div_term = torch.exp(torch.arange(0, d_model, 2).float() * (-math.log(10000.0) / d_model))
        pe[:, 0::2] = torch.sin(position * div_term)
        pe[:, 1::2] = torch.cos(position * div_term)
        pe = pe.unsqueeze(0)
        self.register_buffer('pe', pe)

    def forward(self, x):
        x = x + self.pe[:, :x.size(1)]
        return x
class MultiHeadAttention(nn.Module):
    def __init__(self, d_model, num_heads):
        super(MultiHeadAttention, self).__init__()
        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads

        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, Q, K, V, mask=None):
        batch_size = Q.size(0)

        # 线性变换并分头
        Q = self.W_q(Q).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        K = self.W_k(K).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        V = self.W_v(V).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)

        # 计算注意力分数
        scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(self.d_k)
        if mask is not None:
            scores = scores.masked_fill(mask == 0, -1e9)
        attention = F.softmax(scores, dim=-1)

        # 加权求和
        output = torch.matmul(attention, V)
        output = output.transpose(1, 2).contiguous().view(batch_size, -1, self.d_model)

        # 线性变换
        output = self.W_o(output)
        return output   
 class FeedForward(nn.Module):
    def __init__(self, d_model, d_ff):
        super(FeedForward, self).__init__()
        self.fc1 = nn.Linear(d_model, d_ff)
        self.fc2 = nn.Linear(d_ff, d_model)

    def forward(self, x):
        return self.fc2(F.relu(self.fc1(x)))
 class EncoderLayer(nn.Module):
    def __init__(self, d_model, num_heads, d_ff, dropout=0.1):
        super(EncoderLayer, self).__init__()
        self.self_attn = MultiHeadAttention(d_model, num_heads)
        self.feed_forward = FeedForward(d_model, d_ff)
        self.norm1 = nn.LayerNorm(d_model)
        self.norm2 = nn.LayerNorm(d_model)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x, mask=None):
        # 自注意力 + 残差连接 + 归一化
        attn_output = self.self_attn(x, x, x, mask)
        x = self.norm1(x + self.dropout(attn_output))

        # 前馈神经网络 + 残差连接 + 归一化
        ff_output = self.feed_forward(x)
        x = self.norm2(x + self.dropout(ff_output))
        return x
 class Transformer(nn.Module):
    def __init__(self, src_vocab_size, d_model, num_heads, num_layers, d_ff, max_len, dropout=0.1):
        super(Transformer, self).__init__()
        self.embedding = nn.Embedding(src_vocab_size, d_model)
        self.positional_encoding = PositionalEncoding(d_model, max_len)
        self.encoder_layers = nn.ModuleList([EncoderLayer(d_model, num_heads, d_ff, dropout) for _ in range(num_layers)])
        self.fc = nn.Linear(d_model, src_vocab_size)

    def forward(self, src, src_mask=None):
        # 嵌入层 + 位置编码
        x = self.embedding(src)
        x = self.positional_encoding(x)

        # 编码器层
        for layer in self.encoder_layers:
            x = layer(x, src_mask)

        # 输出层
        output = self.fc(x)
        return output
if __name__=='__main__':
   # 定义超参数
    src_vocab_size = 1000  # 输入词汇表大小
    d_model = 512          # 模型维度
    num_heads = 8          # 多头注意力头数
    num_layers = 6         # 编码器层数
    d_ff = 2048            # 前馈神经网络隐藏层维度
    max_len = 100          # 最大序列长度
    dropout = 0.1          # Dropout 概率
    
    # 初始化模型
    model = Transformer(src_vocab_size, d_model, num_heads, num_layers, d_ff, max_len, dropout)
    
    # 示例输入
    src = torch.randint(0, src_vocab_size, (32, 10))  # (batch_size, seq_len)
    src_mask = None  # 可以自定义掩码
    
    # 前向传播
    output = model(src, src_mask)
    print(output.shape)  # 输出形状: (batch_size, seq_len, src_vocab_size)
```

### 4.1.6 解码器介绍

1、解码器的整体结构

解码器由多个 **解码器层（Decoder Layer）** 堆叠而成，每个解码器层包括以下组件：

**掩码多头自注意力机制（Masked Multi-Head Self-Attention）**

**多头交叉注意力机制（Multi-Head Cross-Attention）**

**前馈神经网络（Feed-Forward Network, FFN）**

**残差连接和归一化层（Residual Connection and Layer Normalization）**

解码器层的详细结构

2.1 掩码多头自注意力机制（Masked Multi-Head Self-Attention）

**作用**：解码器需要对目标序列进行自注意力计算，但为了防止模型在训练时“偷看”未来的信息，需要使用掩码（Mask）来屏蔽未来的位置。

**输入**：目标序列的嵌入表示（通常是上一层的输出）。

**掩码**：一个上三角矩阵，用于屏蔽未来的位置。

2.2 多头交叉注意力机制（Multi-Head Cross-Attention）

**作用**：解码器通过交叉注意力机制从编码器的输出中提取有用的信息。

**输入**：

 **Query**：来自解码器的自注意力输出。

 **Key 和 Value**：来自编码器的输出。

**输出**：加权聚合编码器信息的表示。

2.3 前馈神经网络（Feed-Forward Network, FFN）

**作用**：对交叉注意力机制的输出进行非线性变换，增强模型的表达能力。

**结构**：两个线性变换和一个 ReLU 激活函数。

2.4 残差连接和归一化层

**残差连接**：将输入与输出相加，缓解梯度消失问题。

**归一化层**：对输出进行归一化，稳定训练过程。

解码器的工作流程

以下是解码器的详细工作流程：

3.1 输入

目标序列的嵌入表示（通常是词嵌入 + 位置编码）。

3.2 掩码多头自注意力机制

对目标序列进行自注意力计算。

使用掩码屏蔽未来的位置。

输出形状为 `(batch_size, seq_len, d_model)`。

3.3 多头交叉注意力机制

使用解码器的自注意力输出作为 Query。

使用编码器的输出作为 Key 和 Value。

输出形状为 `(batch_size, seq_len, d_model)`。

3.4 前馈神经网络

对交叉注意力机制的输出进行非线性变换。

输出形状为 `(batch_size, seq_len, d_model)`。

3.5 残差连接和归一化层

在每个子层（自注意力、交叉注意力、前馈神经网络）之后添加残差连接和归一化层。

最终输出形状为 `(batch_size, seq_len, d_model)`。

看代码可能更清楚

```Python
import torch
import torch.nn as nn
import torch.nn.functional as F

class MultiHeadAttention(nn.Module):
    def __init__(self, d_model, num_heads):
        super(MultiHeadAttention, self).__init__()
        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads

        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, Q, K, V, mask=None):
        batch_size = Q.size(0)

        # 线性变换并分头
        Q = self.W_q(Q).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        K = self.W_k(K).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        V = self.W_v(V).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)

        # 计算注意力分数
        scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(self.d_k)
        if mask is not None:
            scores = scores.masked_fill(mask == 0, -1e9)
        attention = F.softmax(scores, dim=-1)

        # 加权求和
        output = torch.matmul(attention, V)
        output = output.transpose(1, 2).contiguous().view(batch_size, -1, self.d_model)

        # 线性变换
        output = self.W_o(output)
        return output

class FeedForward(nn.Module):
    def __init__(self, d_model, d_ff):
        super(FeedForward, self).__init__()
        self.fc1 = nn.Linear(d_model, d_ff)
        self.fc2 = nn.Linear(d_ff, d_model)

    def forward(self, x):
        return self.fc2(F.relu(self.fc1(x)))

class DecoderLayer(nn.Module):
    def __init__(self, d_model, num_heads, d_ff, dropout=0.1):
        super(DecoderLayer, self).__init__()
        self.self_attn = MultiHeadAttention(d_model, num_heads)
        self.cross_attn = MultiHeadAttention(d_model, num_heads)
        self.feed_forward = FeedForward(d_model, d_ff)
        self.norm1 = nn.LayerNorm(d_model)
        self.norm2 = nn.LayerNorm(d_model)
        self.norm3 = nn.LayerNorm(d_model)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x, enc_output, src_mask, tgt_mask):
        # 掩码多头自注意力
        attn_output = self.self_attn(x, x, x, tgt_mask)
        x = self.norm1(x + self.dropout(attn_output))

        # 多头交叉注意力
        attn_output = self.cross_attn(x, enc_output, enc_output, src_mask)
        x = self.norm2(x + self.dropout(attn_output))

        # 前馈神经网络
        ff_output = self.feed_forward(x)
        x = self.norm3(x + self.dropout(ff_output))

        return x

class Decoder(nn.Module):
    def __init__(self, tgt_vocab_size, d_model, num_heads, num_layers, d_ff, max_len, dropout=0.1):
        super(Decoder, self).__init__()
        self.embedding = nn.Embedding(tgt_vocab_size, d_model)
        self.positional_encoding = PositionalEncoding(d_model, max_len)
        self.layers = nn.ModuleList([DecoderLayer(d_model, num_heads, d_ff, dropout) for _ in range(num_layers)])
        self.fc = nn.Linear(d_model, tgt_vocab_size)

    def forward(self, tgt, enc_output, src_mask, tgt_mask):
        # 嵌入层 + 位置编码
        x = self.embedding(tgt)
        x = self.positional_encoding(x)

        # 解码器层
        for layer in self.layers:
            x = layer(x, enc_output, src_mask, tgt_mask)

        # 输出层
        output = self.fc(x)
        return output

# 示例用法
tgt_vocab_size = 4  # 目标词汇表大小
d_model = 2         # 模型维度
num_heads = 2       # 多头注意力头数
num_layers = 2      # 解码器层数
d_ff = 4            # 前馈神经网络隐藏层维度
max_len = 3         # 最大序列长度
dropout = 0.1       # Dropout 概率

# 初始化解码器
decoder = Decoder(tgt_vocab_size, d_model, num_heads, num_layers, d_ff, max_len, dropout)

# 示例输入
tgt = torch.tensor([[0, 1, 2]])  # 目标序列 (batch_size, seq_len)
enc_output = torch.tensor([[[0.2, 0.3], [0.4, 0.5], [0.6, 0.7]]])  # 编码器输出 (batch_size, seq_len, d_model)
src_mask = None  # 编码器掩码
tgt_mask = torch.tensor([[1, 0, 0], [1, 1, 0], [1, 1, 1]])  # 解码器掩码

# 前向传播
output = decoder(tgt, enc_output, src_mask, tgt_mask)
print(output)  # 输出形状: (batch_size, seq_len, tgt_vocab_size)
```

### 4.1.7 transformer的几个问题

#### 1、如何估计参数量

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MGY2NWZhMTE5NDUzMGU1MTRlM2U1MWUyZjM3ZWI4MzRfbENOUlRLY2c1d09zdXBxeVJ4SWxVblhaMno2YWMzUVVfVG9rZW46SHpOdGJqUkNYb3RkVFJ4aVVJRmNXdTVrbnViXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODk1OTk1YzcxMWFiMjllOWVjY2NhOTdkNTI3OGVkZDFfMUl0WUVMNXJLUnpTQlkzaUpONUVXaWdjUmFkZzRlTmNfVG9rZW46VUlscGJucXFqb2p1bnJ4NXBMMmN3clM4blFmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2、Transformer 家族

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDM2MmRhZDNhMWNjM2Y1ZjM5NDhkNGY1NWQ5ZjlkNmZfZkNHeEdkVFZwS2poRWhJdmhxS2h5NG5keDVVdzhNdFNfVG9rZW46VmtpQmJhVDZab0xGU3R4cDFQeWNhZTE3blZlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

- 第一类，Encoder Only（粉色）
- 第二类，Encoder-Decoder（绿色）
- 第三类，Decoder Only（蓝色）

1.1 第一类：Encoder Only

主要由 Google [BERT](https://zhida.zhihu.com/search?content_id=239779124&content_type=Article&match_order=1&q=BERT&zhida_source=entity) 模型家族以及其衍生模型组成。BERT 的全称是 Bidirectional Encoder Representations from Transformers（基于Transformer 的双向编码器表示模型），是由 Google AI 团队于 2018 年 10 月发布的一种预训练模型。

BERT 只使用了 Transformer 的编码器，因为 BERT 的设计目标是“理解文本”，而非“生成文本”，可以简单理解为聚焦在 NLP 的上游任务上，因此使用 Encoder 即可，不需要再引入 Decoder 增加模型结构的复杂度。Encoder 基于 Tranformer 核心的 Self-Attention 机制，能够很好的捕获输入序列所有 Token 的上下文关联关系，进而实现更优秀的语义和语法理解能力。

虽然 BERT 没有使用解码器，但可以通过添加一些线性分类神经网络等，实现一些需要解码器的下游任务，如情感分类、问答等。

1.2 第二类：Encoder-Decoder

Google [T5](https://zhida.zhihu.com/search?content_id=239779124&content_type=Article&match_order=1&q=T5&zhida_source=entity) 是典型的 Encoder-Decoder 模型。这类模型同时使用了 Transformer 的编码器和解码器组件，编码器负责将输入序列编码成一个固定长度的、包含上下文语义理解的内部向量序列，解码器负责将这个内部序列解码成目标的输出。这种架构非常适合 Seq2Seq 类的任务，如机器翻译和语音识别。

PS：不过，我有一个疑问，在机器翻译这类任务中，只使用了 Decoder 的 [GPT](https://zhida.zhihu.com/search?content_id=239779124&content_type=Article&match_order=1&q=GPT&zhida_source=entity) 模型，会和如 T5 这类同时使用 Encoder-Decoder 的模型有明显的差异么，假设训练语料以及训练过程没有差异。

除了 T5，国内智谱（清华）的 GLM/ChatGLM 大模型也属于这个类型。因为包含了编码器和解码器两个组件，其架构最为复杂（注意不代表参数量最大）。

1.3 第三类：Decoder Only

这个类别汇集了诸如 OpenAI GPT、Meta LLaMA（Stanford Alpaca、UC Berkeley Vicuna）、Google PaLM 和 Bard（Gemini）、Claude、TII [Falcon](https://zhida.zhihu.com/search?content_id=239779124&content_type=Article&match_order=1&q=Falcon&zhida_source=entity)、百度文心一言（ERNIE3.0）、百川大模型等一大票的明星。这些模型只使用了 Transformer 解码器，推动者生成式 AI 的蓬勃发展。

关于 Transformer 架构相关的内容，可以进一步参考这个系列的另外两篇文章：《大模型的底层架构：Transformer 初识》和《Transformer 架构解析：Self-Attention》。

## 5、必要的Pytorch知识

### 5.1 Pytorch基础

Pytorch由 Facebook 人工智能研究院于 2017 年推出，具有强大的 GPU 加速张量计算功能，并且能够自动进行微分计算，从而可以使用基于梯度的方法对模型参数进行优化。截至 2022 年 8 月，PyTorch 已经和 Linux 内核、Kubernetes 等并列成为世界上增长最快的 5 个开源社区之一。现在在 NeurIPS、ICML 等等机器学习顶会中，有超过 80% 研究人员用的都是 PyTorch。

#### 5.1.1 张量

张量(Tensor) 是深度学习的基础，例如常见的 0 维张量称为标量 (scalar)、1 维张量称为向量 (vector)、2 维张量称为矩阵 (matrix)。Pytorch 本质上就是一个基于张量的数学计算工具包，它提供了多种方式来创建张量

从 Python 列表创建

```Python
import torch

# 创建 1 维张量（向量）
tensor_1d = torch.tensor([1, 2, 3])
print(tensor_1d)

# 创建 2 维张量（矩阵）
tensor_2d = torch.tensor([[1, 2], [3, 4]])
print(tensor_2d)
```

创建全零或全一张量

```Python
# 创建 2x3 的全零张量
zeros_tensor = torch.zeros(2, 3)
print(zeros_tensor)

# 创建 2x3 的全一张量
ones_tensor = torch.ones(2, 3)
print(ones_tensor)
```

创建随机张量

```Python
# 创建 2x3 的随机张量（值在 0 到 1 之间）
random_tensor = torch.rand(2, 3)
print(random_tensor)

# 创建 2x3 的正态分布随机张量（均值为 0，标准差为 1）
normal_tensor = torch.randn(2, 3)
print(normal_tensor)
```

创建单位矩阵

```Python
# 创建 3x3 的单位矩阵
eye_tensor = torch.eye(3)
print(eye_tensor)
```

张量的属性：

每个张量都有以下属性：

- **形状（Shape）**：张量的维度大小。
- **数据类型（dtype）**：张量中元素的数据类型（如 `float32`, `int64`）。
- **设备（device）**：张量存储在 CPU 还是 GPU 上

```Python
tensor = torch.tensor([[1, 2], [3, 4]])

# 查看张量的形状
print(tensor.shape)  # 输出: torch.Size([2, 2])

# 查看张量的数据类型
print(tensor.dtype)  # 输出: torch.int64

# 查看张量的设备
print(tensor.device)  # 输出: cpu
```

张量的操作：索引和切片

```Python
tensor = torch.tensor([[1, 2, 3], [4, 5, 6]])

# 获取第一行
print(tensor[0])  # 输出: tensor([1, 2, 3])

# 获取第二列
print(tensor[:, 1])  # 输出: tensor([2, 5])

# 获取子矩阵
print(tensor[0:2, 1:3])  # 输出: tensor([[2, 3], [5, 6]])
```

张量的操作：改变形状

`view()` **方法**

- **作用**：返回一个具有新形状的张量，但数据共享。
- **注意**：`view()` 要求新形状的元素总数与原张量一致。
- **示例**

```Python
tensor = torch.tensor([[1, 2], [3, 4]])

# 改变形状为 1x4
reshaped_tensor = tensor.view(1, 4)
print(reshaped_tensor)

# 改变形状为 4x1
reshaped_tensor = tensor.view(4, 1)
print(reshaped_tensor)
```

`reshape()` **方法**

- **作用**：与 `view()` 类似，但更灵活。如果可能，返回一个视图（共享数据）；否则，返回一个副本。
- **注意**：`reshape()` 会自动处理连续性（contiguity）问题。

```Python
tensor = torch.tensor([[1, 2], [3, 4]])
reshaped_tensor = tensor.reshape(1, 4)  # 改变形状为 1x4
print(reshaped_tensor)
```

`unsqueeze()` **方法**

- **作用**：在指定维度上增加一个大小为 1 的维度。
- **示例**

```Python
tensor = torch.tensor([1, 2, 3])
unsqueezed_tensor = tensor.unsqueeze(0)  # 在第 0 维增加一个维度
print(unsqueezed_tensor.shape)  # 输出: torch.Size([1, 3])
```

`squeeze()` **方法**

- **作用**：移除所有大小为 1 的维度，或移除指定维度。
- **示例**：

```Python
tensor = torch.tensor([[1], [2], [3]])
squeezed_tensor = tensor.squeeze()  # 移除大小为 1 的维度
print(squeezed_tensor.shape)  # 输出: torch.Size([3])
```

`permute()` **方法**

- **作用**：重新排列张量的维度顺序。
- **示例**：

```Python
tensor = torch.tensor([[[1, 2], [3, 4]]])  # 形状: (1, 2, 2)
permuted_tensor = tensor.permute(2, 0, 1)  # 改变维度顺序为 (2, 1, 2)
print(permuted_tensor.shape)  # 输出: torch.Size([2, 1, 2])
```

`transpose()` **方法**

- **作用**：交换两个维度的位置。
- **示例**：

```Python
tensor = torch.tensor([[1, 2], [3, 4]])  # 形状: (2, 2)
transposed_tensor = tensor.transpose(0, 1)  # 交换第 0 维和第 1 维
print(transposed_tensor.shape)  # 输出: torch.Size([2, 2])
```

`flatten()` **方法**

- **作用**：将张量展平为一维。
- **示例**：

```Python
tensor = torch.tensor([[1, 2], [3, 4]])
flattened_tensor = tensor.flatten()  # 展平为一维
print(flattened_tensor)  # 输出: tensor([1, 2, 3, 4])
```

`contiguous()` **方法**

- **作用**：确保张量的内存布局是连续的。
- **注意**：某些操作（如 `transpose()`）会改变张量的形状但不改变内存布局，`contiguous()` 可以解决这个问题。
- **示例**：

```Python
tensor = torch.tensor([[1, 2], [3, 4]])
transposed_tensor = tensor.transpose(0, 1)  # 转置
contiguous_tensor = transposed_tensor.contiguous()  # 确保内存连续
print(contiguous_tensor)
```

#### 5.1.2 张量计算

张量加减法

张量加减法是逐元素操作，要求两个张量的形状相同。

```Python
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([[5, 6], [7, 8]])

# 张量加法
add_result = a + b
print(add_result)  # 输出: tensor([[6, 8], [10, 12]])

# 张量减法
sub_result = a - b
print(sub_result)  # 输出: tensor([[-4, -4], [-4, -4]])
```

**张量乘法**

张量乘法包括逐元素乘法和矩阵乘法。

```Python
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([[5, 6], [7, 8]])

# 逐元素乘法
elementwise_mul = a * b
print(elementwise_mul)  # 输出: tensor([[5, 12], [21, 32]])
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([[5, 6], [7, 8]])

# 矩阵乘法
matmul_result = torch.matmul(a, b)
print(matmul_result)  # 输出: tensor([[19, 22], [43, 50]])
```

**张量范数**

范数表示张量的大小，常用的有 L1 范数和 L2 范数。

```Python
a = torch.tensor([[1, 2], [3, 4]])

# L1 范数（绝对值之和）
l1_norm = torch.norm(a, p=1)
print(l1_norm)  # 输出: tensor(10.)

# L2 范数（欧几里得范数）
l2_norm = torch.norm(a, p=2)
print(l2_norm)  # 输出: tensor(5.4772)
```

**张量广播**

广播机制允许不同形状的张量进行运算。

```Python
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([10, 20])

# 广播加法
broadcast_result = a + b
print(broadcast_result)  # 输出: tensor([[11, 22], [13, 24]])
```

**张量拼接**

将多个张量拼接成一个更大的张量。

```Python
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([[5, 6], [7, 8]])

# 水平拼接
concat_result = torch.cat((a, b), dim=1)
print(concat_result)
# 输出:
# tensor([[1, 2, 5, 6],
#         [3, 4, 7, 8]])
```

**张量与 GPU**

可以将张量移动到 GPU 上进行加速计算。

```Python
# 检查是否有可用的 GPU
if torch.cuda.is_available():
    device = torch.device("cuda")  # 使用 GPU
else:
    device = torch.device("cpu")   # 使用 CPU

# 创建张量并移动到 GPU
tensor = torch.tensor([[1, 2], [3, 4]])
tensor = tensor.to(device)
print(tensor.device)  # 输出: cuda:0 (如果 GPU 可用)
```

**张量计算的高级操作**

张量求和（torch.sum(a,dim=1)）

张量求均值（torch.mean(a.float(), dim=0)）

张量最大值和最小值（torch.max(a)，torch.min(a)）

#### 5.1.3 Pytorch实现自动微分

自动微分可以参考下图（详细可以看https://lotabout.me/2023/Auto-Differentiation-Part-2-Implementation/）

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDA1MGQ2MDVhZWYxNDRmMDQ5NjNiNWYwOGMzMzJiMjhfa0hTeGYyd3UwYkpNWnQ1WWg0OGlVaW9Xa0N2UzBTQ0xfVG9rZW46WVZXZmI1eldPb0dvRjF4TlR1QmN3TWtPblllXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

在 PyTorch 中，张量的 `requires_grad` 属性决定了是否需要计算梯度。默认情况下，`requires_grad` 为 `False`

通过前向传播计算损失函数，然后调用 `backward()` 方法自动计算梯度。

PyTorch 会自动构建计算图，记录张量的操作历史。调用 `backward()` 时，PyTorch 会根据计算图反向传播梯度。

```Python
import torch

# 定义变量 x 和 y，并启用自动微分
x = torch.tensor(1.0, requires_grad=True)
y = torch.tensor(2.0, requires_grad=True)

f = x * y + torch.sin(x)

# 前向传播
print("f(x, y):", f.item())  # 输出: f(x, y): 2.84

# 反向传播
f.backward()

# 查看 x 和 y 的梯度
print("∂f/∂x:", x.grad.item())  # 输出: ∂f/∂x: 2.54
print("∂f/∂y:", y.grad.item())  # 输出: ∂f/∂y: 1.0
```

**禁用梯度计算**

使用 `torch.no_grad()`

```Python
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=True)

with torch.no_grad():
    y = x * 2  # 不会记录计算图
    print(y.requires_grad)  # 输出: False
```

使用 `detach()` 方法

```Python
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=True)
y = x.detach()  # 创建一个不需要梯度的张量
print(y.requires_grad)  # 输出: False
```

**梯度清零**

在每次反向传播之前，需要将梯度清零，否则梯度会累积。

```Python
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=True)

# 第一次计算
y = x * 2
z = y.sum()
z.backward()
print(x.grad)  # 输出: tensor([2., 2., 2.])

# 梯度清零
x.grad.zero_()

# 第二次计算
y = x * 3
z = y.sum()
z.backward()
print(x.grad)  # 输出: tensor([3., 3., 3.])
```

# 第二部分：大模型训练

## 1、预训练

可以参考几个开源的项目

### 1.1  Phi2-Chinese-0.2B

https://github.com/charent/Phi2-mini-Chinese

### 1.2 baby-llama2-chinese

https://github.com/DLLXW/baby-llama2-chinese

### 1.3 ChatLM-mini-Chinese

https://github.com/charent/ChatLM-mini-Chinese

### 1.4 **Mini-llm**

https://github.com/jiahe7ay/MINI_LLM?tab=readme-ov-file

### 1.5 llm-action

大模型实践中训练相关的所有教程。从6B到65B，从全量微调到高效微调（LoRA，QLoRA，P-Tuning v2），再到RLHF（基于人工反馈的强化学习） https://github.com/liguodongiot/llm-action?tab=readme-ov-file

## 2、微调

### 2.1 PEFT

**参数高效微调**（PEFT）是一类针对大规模预训练模型（如BERT、GPT、ViT等）的轻量化微调技术，核心目标是通过**仅更新极少量参数**（通常占总参数的0.1%-5%）实现与全参数微调（Full Fine-Tuning）接近的性能，同时显著降低计算资源、存储成本和训练时间。

**核心思想**

**参数冻结**：保持预训练模型的主体参数**冻结（Frozen）**，避免破坏其通用知识。

**轻量适配**：在模型特定位置插入**小型可训练模块**（如Adapter、LoRA、Prefix等），或仅微调**部分层参数**（如偏置项、LayerNorm参数）。

**低秩分解**：利用低秩矩阵（Low-Rank）或稀疏参数化减少新增参数数量

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmI4MDc4ZGViYjM4NjhkYzFhMDNmOWY3YzEyZmU4MzNfQVJPU21ERUFZVlg3UWc1OVlFbEo0SmE5WmJSN3pyaE5fVG9rZW46QVZOVGJ2ZE5jbzFCOFV4Y2JJcWNmZkVEbk5jXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.1.1 **Adapter Tuning**

Adapter Tuning是一种**参数高效微调（Parameter-Efficient Fine-Tuning, PEFT）**方法，旨在通过插入小型可训练模块（Adapter）到预训练模型中，仅训练这些模块和少量原有参数（如LayerNorm层），实现任务适配。**95%以上的预训练参数保持冻结**，显著降低计算和存储成本。Adapter Tuning的方法有很多种，这里我们举出Houlsby et al. ,2019提出的方法，这也是LoRA论文中提及这项技术时所引用的第一篇文章。

核心结构：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDgxN2ViY2M4NjczMGVhZmY1ZWYwY2I0YzFhOTlmMWZfakg4TjRQbEZXcmZmd0M1cmpaaVZwT1NpZ2lOYnMzcmtfVG9rZW46TEU4eWJ6Y2JEb3hWdFl4dWMyeGN1WWlOblBiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDQ2NTQ4Y2U4N2U1MDc0MzkwODdmODkxZDgzZGVkNTFfdFVYbDM2WEFhQlFLOW1vdTJQOWZCRUExUmJYamN1blRfVG9rZW46UFYyOWJrUXhNb0gzTTZ4ZFpRdmN3bmkybmJQXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

**实践指南**

- **插入位置**：Transformer层的FFN之后或注意力之后（不同任务可能效果不同）。
- **瓶颈维度r**：通常取32-256，需通过验证集调整。
- **初始化策略**：上投影层初始化为近零矩阵，避免干扰原始输出。
- **代码示例（PyTorch）**：

```Python
class Adapter(nn.Module):
    def __init__(self, d_model, r=64):
        super().__init__()
        self.down = nn.Linear(d_model, r)
        self.up = nn.Linear(r, d_model)
        self.act = nn.GELU()
        
    def forward(self, x):
        return x + self.up(self.act(self.down(x)))
```

**局限性**

- **推理延迟**：额外计算Adapter模块。
- **任务冲突**：多任务Adapter间干扰。

解释：

a. 共享主干表示干扰

主干参数冻结但激活被修改： Adapter插入到Transformer层中，虽然主干参数（如权重矩阵）被冻结，但每层的输入/输出激活值会被不同任务的Adapter修改。当多个任务的Adapter作用于同一层时，可能扭曲共享的特征表示，导致不同任务对特征空间的调整方向冲突。 示例：

 任务A（情感分析）需要强化句子级情感特征。

 任务B（实体识别）需关注词级实体位置特征。 若两个任务共享同一层的Adapter，该层输出的特征可能被两个任务的不同需求拉扯，导致两者效果均下降。

b. 梯度更新方向矛盾

多任务联合训练时的梯度冲突： 当同时优化多个任务的Adapter（如多任务学习），不同任务的梯度可能对共享的Adapter参数提出相反的更新方向，导致优化过程震荡或收敛困难。 数学体现： 假设任务1的梯度为∇θL1∇*θ*L1，任务2的梯度为∇θL2∇*θ*L2，若∇θL1∇*θ*L1与∇θL2∇*θ*L2方向相反，则参数更新可能相互抵消。

- **超参数敏感**：需调整r和插入位置。

#### 2.1.2 **Prefix Tuning**

参考https://mp.weixin.qq.com/s/jk1qBRjiq80nK0e04LQqiw

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MzIxMDViZmQ5Y2RiMTk2OGNhYzc2ZTZmYWY2NTk5ZWFfMzRBZ2FlSllLVGJ1VDM0eXplWTdzVGRDYkNaVWpoYXJfVG9rZW46TlVlUWJoR0RDbzI4N2J4c3VBQWNQRkx0blJhXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

Prefix Tuning的方法也有很多种，这里我们选取Li&Liang,2021这一篇进行简述。在这篇中，作者通过对输入数据增加前缀（prefix）来做微调。当然，prefix也可以不止加载输入层，还可以加在Transformer Layer输出的中间层，感兴趣的朋友可以查找论文自行研究。

如图所示，对于**GPT这样的生成式模型**，在输入序列的最前面加入prefix token，图例中加入2个prefix token，在实际应用中，prefix token的个数是个超参，可以根据模型实际微调效果进行调整。**对于BART这样的Encoder-Decoder架构模型**，则在x和y的前面同时添加prefix token。**在后续微调中，我们只需要冻住模型其余部分，单独训练prefix token相关的参数即可，每个下游任务都可以单独训练一套prefix token。**

**那么prefix的含义是什么呢**？prefix的作用是引导模型提取x相关的信息，进而更好地生成y。例如，我们要做一个**summarization**的任务，那么经过微调后，prefix就能领悟到当前要做的是个“总结形式”的任务，然后引导模型去x中提炼关键信息；如果我们要做一个**情感分类**的任务，prefix就能引导模型去提炼出x中和情感相关的语义信息，以此类推。这样的解释可能不那么严谨，但大家可以大致体会一下prefix的作用。

Prefix Tuning虽然看起来方便，但也存在以下两个**显著劣势**：

- 较难训练，且模型的效果并不严格随prefix参数量的增加而上升，这点在原始论文中也有指出
- 会使得输入层有效信息长度减少。为了节省计算量和显存，我们一般会固定输入数据长度。增加了prefix之后，留给原始文字数据的空间就少了，因此可能会降低原始文字中prompt的表达能力。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmU3YjI5NGU4NTY4YjMzNzVhNzVlNGUxMTc3ZGE0MmJfWjExSWRSbm4wN2VYdGpsR0ladzhrOGdBUm9vR1hyZWNfVG9rZW46REdiZmIwR2xCb0VCdVd4U0lUbmM4ZXRrbnFjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.1.3 LoRA

##### LoRA

总结一下，全参数微调太贵，Adapter Tuning存在训练和推理延迟，Prefix Tuning难训且会减少原始训练数据中的有效文字长度，那是否有一种微调办法，能改善这些不足呢？在这样动机的驱动下，作者提出了LoRA (Low-Rank Adaptation，低秩适配器) 这样一种微调方法。

LoRA整体架构

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MzQ0ZDAzM2VjMWU3ZTM2ZjUzYjFjZmE2ZjdjZTlhZDFfMUxVSW1ucmtJQWZpODd5SWk1MWNORFB6YU5WTFhEV1pfVG9rZW46UUpNRGJVSG5nb2tVSjl4R3lyVGNNSXpwbldnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NzI1ZmNjOTYyMTAyYjZiYTU0MjAzMjJlMzY0OWJmYzZfdGhQbHZuZ0x1RDdoc25rdjRBUzNqdUUwYjQ0S0NBZHNfVG9rZW46RFRscmJGVDBKb2pyaVl4VmZOTmNIS3hrbmZlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

A和B的初始化方法

需要注意的是，这里对采用高斯初始化，对采用零初始化的目的是，让训练刚开始时的值为0，这样不会给模型带来额外的噪声。那么你可能想问，那我对做零初始化，对做高斯初始化行不行呢？反正看起来只要让初始化为0就行？

当前作者还没有发现转换初始化方式产生的显著区别，只要这两者中任意一者为0，另一者不为0即可。

数学推导：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWFlODAwYjQ5ZmFmYzIyNWE1YzU3NTRiNjBiODdjN2JfZ01pbzlZcG1hRzFIS3hWSW41SHJmS09oRzlZMlhjVVdfVG9rZW46UFpaRWJYNUZsb2VWbjF4VlMzVGN3U0l6bjhyXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

例子：基于预训练BERT的LoRA微调

```Python
from transformers import AutoModelForSequenceClassification, Trainer, TrainingArguments
from datasets import load_dataset
import torch
from torch import nn

# 1. 加载预训练模型
model = AutoModelForSequenceClassification.from_pretrained("bert-base-uncased", num_labels=2)

# 2. 冻结所有原始参数
for param in model.parameters():
    param.requires_grad = False

# 3. 定义LoRA层（替换原有关键层的线性投影）
class LoRALayer(nn.Module):
    def __init__(self, original_layer, rank=8):
        super().__init__()
        self.original_layer = original_layer  # 原BERT的Linear层（冻结）
        self.rank = rank
        d_in, d_out = original_layer.weight.shape
        
        # 初始化LoRA参数
        self.A = nn.Parameter(torch.randn(d_in, rank))
        self.B = nn.Parameter(torch.zeros(rank, d_out))
        
    def forward(self, x):
        orig_out = self.original_layer(x)
        lora_out = (x @ self.A) @ self.B
        return orig_out + lora_out

# 4. 将BERT的query和value投影层替换为LoRA版本
for layer in model.bert.encoder.layer:
    layer.attention.self.query = LoRALayer(layer.attention.self.query, rank=8)
    layer.attention.self.value = LoRALayer(layer.attention.self.value, rank=8)

# 5. 验证参数可训练性
total_params = sum(p.numel() for p in model.parameters())
trainable_params = sum(p.numel() for p in model.parameters() if p.requires_grad)
print(f"可训练参数占比: {trainable_params}/{total_params} ({trainable_params/total_params:.2%})")  
# 输出示例：可训练参数占比: 393,216/109,514,298 (0.36%)

# 6. 准备数据集
dataset = load_dataset("glue", "sst2")
dataset = dataset.map(lambda e: tokenizer(e["sentence"], truncation=True, padding="max_length"), batched=True)

# 7. 训练配置
training_args = TrainingArguments(
    output_dir="./results",
    learning_rate=3e-4,  # LoRA通常需要更大的学习率
    per_device_train_batch_size=32,
    num_train_epochs=3,
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=dataset["train"],
    eval_dataset=dataset["validation"],
)

# 8. 开始微调
trainer.train()

# 9. 合并LoRA权重（可选）
def merge_lora_weights(model):
    for layer in model.bert.encoder.layer:
        # 合并query层的LoRA
        delta_w = layer.attention.self.query.A @ layer.attention.self.query.B
        layer.attention.self.query.original_layer.weight.data += delta_w.T
        
        # 合并value层的LoRA
        delta_w = layer.attention.self.value.A @ layer.attention.self.value.B
        layer.attention.self.value.original_layer.weight.data += delta_w.T

merge_lora_weights(model)
model.save_pretrained("bert-lora-sst2")  # 保存完整模型
```

LoRA低秩适配原理和超参数a的解释，见https://mp.weixin.qq.com/s/jk1qBRjiq80nK0e04LQqiw

##### AdaLoRA

1. **背景与原理**

**AdaLoRA**（Adaptive Low-Rank Adaptation）是 LoRA（Low-Rank Adaptation）的改进版本，主要用于高效微调大语言模型（如 GPT、LLaMA 等）。其核心思想是 **动态调整参数更新的秩（Rank）**，在不同网络层或训练阶段分配不同的计算资源，从而在保持性能的同时减少计算开销。

**核心机制**

1. **低秩分解**（LoRA 基础）
2. **自适应秩分配（AdaLoRA 的创新）**
   1. AdaLoRA 动态调整每层的秩 *r*：
      - 对重要层分配更高的秩（保留更多参数），对次要层分配更低的秩。
      - 通过 **参数重要性评分**（如梯度敏感度或参数对损失的贡献）动态调整各层的秩。
3. **参数重要性评估**
   1. 使用 **Hessian矩阵** 或 **梯度统计量** 评估参数重要性。
   2. 重要性高的参数分配更多资源（高秩），反之则裁剪低重要性参数。
4. **具体实现**

**步骤 1**：初始化所有层的低秩矩阵 A*A* 和 B*B*，并设定总参数预算（如总秩数上限）。

**步骤 2**：在训练过程中，定期计算每层参数的重要性得分。

**步骤 3**：根据得分重新分配各层的秩（例如，裁剪低重要性层的秩，分配给高重要性层）。

**步骤 4**：冻结裁剪后的参数，继续训练剩余参数。

5、**示例说明**

**场景**：微调一个 GPT-2 模型用于文本分类任务，总参数预算为秩 Rtotal=100。

- **初始设置**： 假设模型有 12 层 Transformer，每层初始分配秩 *r*=8，总秩 12×8=96，剩余 4 秩作为缓冲。
- **动态调整**： 训练过程中，通过计算发现：
  - 第 3 层和第 6 层的参数对损失影响最大（重要性高）。
  - 第 1 层和第 9 层的参数重要性较低。
- 调整后：
  - 第 3 层和第 6 层的秩增加到 *r*=12。
  - 第 1 层和第 9 层的秩减少到*r*=4。
  - 总秩保持 2×12+2×4+8×8=100。
- **结果**：
  - 模型性能接近全参数微调，但可训练参数减少 90% 以上。
  - 训练速度提升，显存占用降低。

##### QLoRA

1. **背景与原理**

**QLoRA**（Quantized Low-Rank Adaptation）是 LoRA 的量化扩展版本，旨在 **同时降低显存占用和计算开销**，适用于在资源受限设备（如单张消费级 GPU）上微调超大规模语言模型（如 LLaMA-65B）。其核心创新在于 **将模型权重量化存储，同时通过低秩适配器进行高效参数更新**。

**核心机制**

1. **权重量化（Quantization）**
   1. 将预训练模型的原始权重（如 FP16 或 BF16）压缩为 **4 位精度存储**，显存占用减少至 1/4。
   2. 量化方法：采用 **分块动态量化**（Block-wise Dynamic Quantization），将权重矩阵分为小块，每块单独计算缩放因子（Scale）和零点（Zero Point），以减少量化误差。
2. **反量化计算（Dequantization）**
   1. 前向传播时，将量化权重动态反量化为高精度（如 BF16），叠加适配器增量后执行计算，以保持数值稳定性。
3. **优化器内存优化**
   1. 使用 **4 位量化存储主权重** + **NF4（Normalized Float 4）格式优化**，结合 **双量化（Double Quantization）** 技术，进一步压缩优化器状态（如梯度、动量）的显存占用。

**具体实现**

**步骤 1**：将预训练模型权重量化为 4 位（分块动态量化）。

**步骤 2**：为需要微调的层（如注意力模块）添加低秩适配器 A*A* 和 B*B*。

**步骤 3**：训练时，动态反量化权重，计算梯度并仅更新适配器参数。

**步骤 4**：推理时，合并量化权重与适配器增量，或直接保留适配器结构。

**示例说明**

**场景**：在单张 24GB 显存的 RTX 4090 上微调 LLaMA-7B 模型（原始显存需求约 14GB FP16）。

- **QLoRA 配置**：
  - 主权重：4 位分块量化（占用约 3.5GB）。
  - 适配器：每层添加秩 r=64的 LoRA 矩阵（可训练参数约 0.1% 的模型参数量）。
  - 优化器：使用 4 位 AdamW，显存占用降低 60%。
- **显存分配**：
  - 量化权重：3.5GB
  - 适配器参数 + 梯度：2GB
  - 优化器状态：5GB
  - 激活值 + 其他：8GB
  - **总计**：约 18.5GB（可在 24GB GPU 上运行）。
  - ![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDUzYjBlMWQwMGQyYTQ1YWEyYjgwZjUxOTliNTE2OWVfaksyQzdVUlhXaElEeUhIQzF4cU1rekM1OUtDQ0xqY2FfVG9rZW46VGRvWWJsYWJ3bzh0T1Z4NnE0Q2NkYUVNbkVkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 2.1.4 **Prompt Tuning**

 **核心思想**

Prompt Tuning 是一种 参数高效微调（Parameter-Efficient Fine-Tuning, PEFT） 方法，旨在通过调整少量参数（而非整个模型）来适配下游任务。其核心思想是：

- 在**输入序列**前添加可学习的**「软提示」（Soft Prompts）**：这些提示是虚拟的、**连续的向量**（而非真实文本），通过梯度下降优化它们的嵌入表示。
- 冻结预训练模型参数：仅更新软提示对应的参数，模型主体保持固定。
- 通过提示引导模型输出：软提示在输入中隐式地调整模型的注意力分布，从而控制生成或分类结果

**技术实现细节**

(1) 软提示的构造

参数形式：软提示是一组可学习的向量矩阵，维度为 `[prompt_length × hidden_size]`（与模型的嵌入维度一致）。

初始化方式：

 随机初始化：直接随机初始化向量。

 基于真实词初始化：选择与任务相关的关键词（如 "translate to French"）的嵌入作为初始值。

(2) 输入拼接

将软提示向量拼接在输入文本的嵌入序列前，形成新的输入：

输入 = [软提示1, 软提示2, ..., 软提示N, 文本token1, 文本token2, ...]

关键点：软提示的向量会参与模型的全部计算（如注意力机制），但只有这些向量的参数会被更新。

(3) 训练过程

仅优化软提示参数：模型的其他参数被冻结，反向传播时仅计算软提示的梯度。

损失函数：根据任务类型设计（如交叉熵损失用于分类任务，负对数似然用于生成任务）。

例子：

```Python
import torch
from torch import nn
from transformers import AutoTokenizer, AutoModelForSequenceClassification
from torch.optim import AdamW

# 示例参数
MODEL_NAME = "t5-small"  # 也可替换为 "bert-base-uncased" 等
PROMPT_LENGTH = 10       # 软提示长度
BATCH_SIZE = 4
LR = 1e-3
class PromptTuningModel(nn.Module):
    def __init__(self, model_name, prompt_length, num_labels):
        super().__init__()
        # 加载预训练模型（冻结参数）
        self.model = AutoModelForSequenceClassification.from_pretrained(model_name, num_labels=num_labels)
        for param in self.model.parameters():
            param.requires_grad = False  # 冻结模型参数
        
        # 定义软提示参数
        self.prompt_length = prompt_length
        hidden_size = self.model.config.hidden_size  # 获取模型隐藏层维度
        self.prompt_embeddings = nn.Parameter(
            torch.randn(prompt_length, hidden_size)  # 随机初始化软提示
        )
        
    def forward(self, input_ids, attention_mask):
        # 获取输入文本的嵌入
        inputs_embeds = self.model.get_input_embeddings()(input_ids)
        
        # 拼接软提示与输入文本
        batch_size = input_ids.size(0)
        prompt_embeds = self.prompt_embeddings.unsqueeze(0).repeat(batch_size, 1, 1)
        combined_embeds = torch.cat([prompt_embeds, inputs_embeds], dim=1)
        
        # 调整注意力掩码（包含软提示部分）
        prompt_mask = torch.ones(batch_size, self.prompt_length).to(attention_mask.device)
        combined_mask = torch.cat([prompt_mask, attention_mask], dim=1)
        
        # 前向传播
        outputs = self.model(inputs_embeds=combined_embeds, attention_mask=combined_mask)
        return outputs.logits
 tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME)

# 示例数据（情感分类：0=Negative, 1=Positive）
texts = ["I love this movie!", "This product is terrible..."]
labels = [1, 0]

# 编码文本
inputs = tokenizer(
    texts, 
    padding=True, 
    truncation=True, 
    return_tensors="pt", 
    max_length=128  # 控制文本最大长度
)
input_ids = inputs["input_ids"]
attention_mask = inputs["attention_mask"]
labels = torch.tensor(labels)
model = PromptTuningModel(MODEL_NAME, PROMPT_LENGTH, num_labels=2)
optimizer = AdamW([model.prompt_embeddings], lr=LR)  # 仅优化软提示参数
loss_fn = nn.CrossEntropyLoss()

# 简单训练步骤（示例）
for epoch in range(5):
    model.train()
    optimizer.zero_grad()
    
    logits = model(input_ids, attention_mask)
    loss = loss_fn(logits, labels)
    loss.backward()
    optimizer.step()
    
    print(f"Epoch {epoch+1}, Loss: {loss.item():.4f}")
```

#### 2.1.5 P-Tuning

##### P-Tuning-v1

P-Tuning（论文：GPT Understands, Too），该方法将Prompt转换为可以学习的Embedding层，并用MLP+LSTM的方式来对Prompt Embedding进行一层处理。

相比Prefix Tuning，P-Tuning加入的可微的virtual token，但仅限于输入层，没有在每一层都加；另外，virtual token的位置也不一定是前缀，插入的位置是可选的。这里的出发点实际是把传统人工设计模版中的真实token替换成可微的virtual token。

经过预训练的LM的词嵌入已经变得高度离散，如果随机初始化virtual token，容易优化到局部最优值，而这些virtual token理论是应该有相关关联的。因此，作者通过实验发现用一个prompt encoder来编码会收敛更快，效果更好。即用一个LSTM+MLP去编码这些virtual token以后，再输入到模型。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MDQ1OTBjZmE4MTYxOGFjYjZjMTE0ZjA0NTg4MWRhOGRfNmd1QWJ4T01ndWpwZjFEaWgyYzl1UGhJSGhMWTZ6TUtfVG9rZW46RU1pY2JoRnJyb0lPTHh4MVJkdmNjd1pCbmpmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

##### P-Tuning v2

之前的Prompt Tuning和P-Tuning等方法存在两个主要的问题：

第一，缺乏模型参数规模和任务通用性。

- 缺乏规模通用性：Prompt Tuning论文中表明当模型规模超过100亿个参数时，提示优化可以与全量微调相媲美。但是对于那些较小的模型（从100M到1B），提示优化和全量微调的表现有很大差异，这大大限制了提示优化的适用性。
- 缺乏任务普遍性：尽管Prompt Tuning和P-tuning在一些 NLU 基准测试中表现出优势，但提示调优对硬序列标记任务（即序列标注）的有效性尚未得到验证。

第二，缺少深度提示优化，在Prompt Tuning和P-tuning中，连续提示只被插入transformer第一层的输入embedding序列中，在接下来的transformer层中，插入连续提示的位置的embedding是由之前的transformer层计算出来的，这可能导致两个可能的优化挑战。

- 由于序列长度的限制，可调参数的数量是有限的。
- 输入embedding对模型预测只有相对间接的影响。

考虑到这些问题，作者提出了Ptuning v2，它利用深度提示优化（如：Prefix Tuning），对Prompt Tuning和P-Tuning进行改进，作为一个跨规模和NLU任务的通用解决方案。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODIzZjAyNGEwODE1NWQ2M2RmN2Y0MGFiNjlkMzFkYzRfTERpME1EMlhXMHVGOUZKaGR1eVhuQkdxaVN3c3ZmcGhfVG9rZW46Q2RFaGI4ZGk0b2hrSzV4RnNXNmMyNExsbm9mXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

### 2.2 详解RLHF、PPO、DPO

非常详细，建议细度

https://mp.weixin.qq.com/s/mhPJzhQvPJlAWsO2nW9BHg

https://mp.weixin.qq.com/s/aG-5xTwSzvHXN4B73mfKMA

### 2.3 微调框架和工具

#### **1、Hugging Face 生态工具**

##### **a. Transformers + Trainer/Accelerate**

- **特点**：Hugging Face 的 `transformers` 库是 NLP 领域的标准工具，内置 `Trainer` 类和 `accelerate` 库，支持分布式训练和混合精度。
- **适用场景**：适合快速实现经典模型（如 BERT、GPT-2）的微调。

代码示例（全量参数微调）

```Python
# 安装必要库
# pip install transformers datasets evaluate accelerate

from datasets import load_dataset
from transformers import (
    AutoTokenizer,
    AutoModelForSequenceClassification,
    TrainingArguments,
    Trainer,
    DataCollatorWithPadding
)
import evaluate
import numpy as np

# 1. 加载数据集（以IMDB情感分析为例）
dataset = load_dataset("imdb")
print(dataset["train"][0])  # 查看样例数据

# 2. 加载Tokenizer
model_name = "bert-base-uncased"
tokenizer = AutoTokenizer.from_pretrained(model_name)

# 预处理函数
def preprocess_function(examples):
    return tokenizer(
        examples["text"],
        truncation=True,
        max_length=256,
    )

# 预处理数据集
tokenized_dataset = dataset.map(
    preprocess_function,
    batched=True,
    remove_columns=["text"]  # 移除原始文本列
)

# 创建数据收集器（动态填充）
data_collator = DataCollatorWithPadding(tokenizer=tokenizer)

# 3. 加载模型
model = AutoModelForSequenceClassification.from_pretrained(
    model_name,
    num_labels=2  # 分类任务标签数
)

# 4. 配置训练参数
training_args = TrainingArguments(
    output_dir="./results",
    evaluation_strategy="epoch",
    learning_rate=2e-5,
    per_device_train_batch_size=16,
    per_device_eval_batch_size=16,
    num_train_epochs=3,
    weight_decay=0.01,
    save_strategy="epoch",
    load_best_model_at_end=True,
    logging_dir='./logs',
    logging_steps=50,
    report_to="none"  # 禁用第三方日志（可选）
)

# 5. 定义评估指标
metric = evaluate.load("accuracy")

def compute_metrics(eval_pred):
    logits, labels = eval_pred
    predictions = np.argmax(logits, axis=-1)
    return metric.compute(predictions=predictions, references=labels)

# 6. 初始化Trainer
trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_dataset["train"],
    eval_dataset=tokenized_dataset["test"],
    data_collator=data_collator,
    tokenizer=tokenizer,
    compute_metrics=compute_metrics,
)

# 7. 开始训练
trainer.train()

# 8. 评估模型
results = trainer.evaluate()
print(f"最终评估准确率: {results['eval_accuracy']:.2%}")

# 9. 保存模型
trainer.save_model("./my_finetuned_bert")
```

使用Accelerate的分布式训练版本（补充）

```Python
from accelerate import Accelerator
from torch.utils.data import DataLoader

# 初始化加速器
accelerator = Accelerator()

# 创建数据加载器
train_dataloader = DataLoader(
    tokenized_dataset["train"],
    shuffle=True,
    collate_fn=data_collator,
    batch_size=16
)

eval_dataloader = DataLoader(
    tokenized_dataset["test"],
    collate_fn=data_collator,
    batch_size=16
)

# 准备模型和优化器
model, optimizer, train_dl, eval_dl = accelerator.prepare(
    model,
    AdamW(model.parameters(), lr=2e-5),
    train_dataloader,
    eval_dataloader
)

# 自定义训练循环
for epoch in range(3):
    model.train()
    for batch in train_dl:
        outputs = model(**batch)
        loss = outputs.loss
        accelerator.backward(loss)
        optimizer.step()
        optimizer.zero_grad()

    model.eval()
    for batch in eval_dl:
        with torch.no_grad():
            outputs = model(**batch)
        logits = outputs.logits
        predictions = torch.argmax(logits, dim=-1)
        accelerator.gather_for_metrics((predictions, batch["labels"]))
```

##### **b. TRL (Transformer Reinforcement Learning)**

- **特点**：专为强化学习微调（如 RLHF）设计，支持 SFT、PPO、DPO 等算法。
- **适用场景**：需要对齐人类反馈的模型（如 ChatGPT 风格模型）。
- **GitHub**：https://github.com/huggingface/trl

代码示例1

```Python
from trl import SFTConfig, SFTTrainer
from datasets import load_dataset

dataset = load_dataset("trl-lib/Capybara", split="train")

training_args = SFTConfig(output_dir="Qwen/Qwen2.5-0.5B-SFT")
trainer = SFTTrainer(
    args=training_args,
    model="Qwen/Qwen2.5-0.5B",
    train_dataset=dataset,
)
trainer.train()
```

代码示例2

```Python
from datasets import load_dataset
from trl import GRPOConfig, GRPOTrainer

dataset = load_dataset("trl-lib/tldr", split="train")

# Dummy reward function: rewards completions that are close to 20 characters
def reward_len(completions, **kwargs):
    return [-abs(20 - len(completion)) for completion in completions]

training_args = GRPOConfig(output_dir="Qwen2-0.5B-GRPO", logging_steps=10)
trainer = GRPOTrainer(
    model="Qwen/Qwen2-0.5B-Instruct",
    reward_funcs=reward_len,
    args=training_args,
    train_dataset=dataset,
)
trainer.train()
```

#### 2、 **参数高效微调 (PEFT)**

##### **a. PEFT 库**

- **特点**：支持 LoRA、Adapter、Prompt Tuning 等低资源微调方法，显存占用低。
- **适用场景**：资源有限时微调大模型（如 LLaMA、Mistral）。

**代码示例**：

```Python
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import PrefixTuningConfig, get_peft_model

# 加载预训练生成模型（如GPT-2）
model = AutoModelForCausalLM.from_pretrained("gpt2")
tokenizer = AutoTokenizer.from_pretrained("gpt2")

# 配置Prefix-Tuning
peft_config = PrefixTuningConfig(
    task_type="CAUSAL_LM",
    num_virtual_tokens=30,  # 前缀令牌长度
    encoder_hidden_size=512 # 若为双向模型需配置
)

# 获取PEFT模型
peft_model = get_peft_model(model, peft_config)

# 检查可训练参数比例
peft_model.print_trainable_parameters()
# 输出示例：0.09%参数可训练
# 结合Transformers Trainer的最佳实践
from transformers import TrainingArguments, Trainer
# 加速参数设置
training_args = TrainingArguments(
    output_dir="peft_output",
    learning_rate=3e-4,       # PEFT需更高学习率（相对于全参数微调）
    per_device_train_batch_size=16,
    gradient_accumulation_steps=2,  # 优化显存使用
    fp16=True,                # 半精度训练 
    logging_steps=10,
    num_train_epochs=5,
)

trainer = Trainer(
    model=peft_model,
    args=training_args,
    train_dataset=dataset,
)

# 启动训练
trainer.train()

# 保存适配器权重
peft_model.save_pretrained("./adapter_weights")
```

##### **b. Unsloth**

- **特点**：针对 LoRA 优化的加速框架，训练速度提升 2-5 倍，显存减少 70%。
- **适用场景**：需要快速迭代的 LoRA 微调。
- **GitHub**：https://github.com/unslothai/unsloth

#### **3. 分布式训练框架**

##### **a. DeepSpeed**

- **特点**：微软开发的分布式训练框架，支持 ZeRO 优化、3D 并行（数据/流水线/模型并行）。
- **适用场景**：超大规模模型（如 10B+ 参数量）的高效训练。
- **链接**：https://www.deepspeed.ai/

##### **b. Megatron-LM**

- **特点**：NVIDIA 的分布式训练框架，优化 Transformer 架构。
- **适用场景**：GPU 集群上的大规模训练。
- **GitHub**：https://github.com/NVIDIA/Megatron-LM

#### **4. 轻量级工具**

##### **a. Axolotl**

- **特点**：一键式微调框架，支持多种模型（LLaMA、Mistral、Phi），集成 LoRA、QLoRA、FSDP。
- **优点**：配置简单，适合快速实验。
- **GitHub**：https://github.com/OpenAccess-AI-Collective/axolotl

##### **b. Lit-GPT**

- **特点**：轻量化的 PyTorch 实现，支持量化微调（QLoRA）、Flash Attention。
- **适用场景**：需要高度定制化代码的研究场景。
- **GitHub**：https://github.com/Lightning-AI/lit-gpt

#### **5. 特定模型优化框架**

- **LLaMA-Factory**：专为 LLaMA、BLOOM 等模型设计，支持多种高效微调方法。
  - GitHub：https://github.com/hiyouga/LLaMA-Factory
- **MosaicML Composer**：支持 LLM 全流程训练，集成高效算法。
  - 链接：https://www.mosaicml.com/composer

#### 6、**选择建议**

1. **快速实验**：Axolotl 或 LLaMA-Factory（配置简单）。
2. **低资源场景**：PEFT + QLoRA（8GB 显存即可微调 7B 模型）。
3. **大规模分布式训练**：DeepSpeed/Megatron-LM。
4. **强化学习对齐**：TRL + PPO/DPO。

### 2.4、PEFT、SFT、RLHF对比

**三大调优方法对比矩阵**

| 维度     | PEFT（参数高效微调）               | SFT（监督微调）           | RLHF（人类反馈强化学习）                |
| -------- | ---------------------------------- | ------------------------- | --------------------------------------- |
| 核心技术 | LoRA/Adapter等参数节约方法         | 全参数监督式训练          | PPO算法+人类反馈奖励模型                |
| 训练目标 | 微调部分参数适配下游任务           | 最小化交叉熵损失          | 最大化人工标注的奖励信号                |
| 数据需求 | 1-5k样本（少样本学习）             | 1-100k（根据任务复杂度）  | 需要专家标注偏好数据（成本高）          |
| 计算成本 | 10%参数更新，单卡可训（显存<24GB） | 全参数更新，需要多卡并行  | 需多阶段训练（SFT+RM+RL），显存需求最高 |
| 典型场景 | 多任务适配/小数据集/边缘设备部署   | 垂直领域精调（医疗/法律） | 安全对齐/价值观修正/内容安全性          |
| 优点     | 避免灾难性遗忘/轻量化部署          | 任务拟合能力强            | 输出更符合人类偏好                      |
| 缺点     | 复杂任务表现受限                   | 数据质量敏感/易过拟合     | 训练流程复杂/反馈成本高昂               |
| 开源工具 | HuggingFace PEFT库                 | Transformers Trainer      | TRL/DeepSpeed Chat                      |
| 时延增加 | 1.1-1.3倍（LoRA线性层扩展）        | 无                        | 3-5倍（需运行奖励模型）                 |

三个方法也可混合使用

**三大组合范式与适用场景**

| 组合模式    | 核心优势               | 典型场景                 | 技术实现路径                                        |
| ----------- | ---------------------- | ------------------------ | --------------------------------------------------- |
| SFT → PEFT  | 兼顾深度适应与灵活扩展 | 多任务企业级系统         | 1) SFT全参数领域预训练 2) PEFT适配各业务线          |
| SFT → RLHF  | 确保安全可靠的复杂决策 | 医疗/法律/金融等高危领域 | 1) SFT构建基础能力 2) RLHF对齐专业标准              |
| PEFT → RLHF | 轻量化解决方案         | 移动端应用/边缘计算      | 1) PEFA快速适配硬件 2) RLHF精简奖励模型优化关键指标 |

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MmZjMzhmZGM2YzdkZDg2ZmRmMDdhNmE2OTI3MzA1MTlfb0tBRnM4UFJtc2tNaUNSTVFacEl1Z3NLSGFzaGtkUEFfVG9rZW46TGRJbWJqelBtb2dMNTd4NmpScmNIQXc5bmpmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

# 第三部分：大模型推理

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YjQxMGUyMzhiNmZjNzMwZGZkOGMyYTNhNDIyOGUxMzlfVEJkV3VTWVpMWk96d3VSUTNKZldxVnJzZkJ3QWFYSUxfVG9rZW46RVdoaWJOeDdWb29hNGx4cW5HYWNCTXJvbnljXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 1、**Kv cache**

### **原理**

在 Transformer 模型的自回归推理中，模型一次生成一个 token，并将其加入到输入序列的末尾，作为下一次生成的上下文。这种生成方式意味着，对于每个新生成的 token，模型都需要重新计算整个输入序列的注意力表示。这样做存在大量的冗余计算，因为除了最后一个 token，其他 token 的注意力表示在连续的生成步骤中是重复的。

KV Cache 的核心思想是缓存之前生成的 token 的 Key 和 Value 向量，这样在生成下一个 token 时，就不需要重新计算这些已经存在的表示。因为 Key 和 Value 向量在序列生成过程中变化不大，所以可以有效地减少重复计算，提高推理速度。

### **工作流程**

1. **初始化**：在生成序列的开始，模型会将整个输入序列输入到 Transformer 模型中，计算得到每个 token 的 Key、Value 和 Query 向量，并存储下来作为初始的 KV Cache。
2. **生成下一个 token**：当模型生成下一个 token 时，只需要将当前的最后一个 token 通过 Embedding 层映射成 q\k\v，而不需要重新计算 之前token的Key 和 Value 向量。
3. **利用 KV Cache**：模型使用当前 token 的 Query 向量与缓存中的 Key 和 Value 向量进行注意力计算，得到当前 token 的注意力表示。
4. **更新缓存**：生成新的 token 后，模型会将新 token 的 Key 和 Value 向量添加到 KV Cache 中，以便在后续的生成步骤中使用。
5. **重复步骤**：重复步骤 2 至 4，直到生成完整的序列。

### **优点**

- **提高效率**：通过缓存 Key 和 Value 向量，减少了重复计算，显著提高了推理速度。
- **节省内存**：由于不需要在每次生成时重新计算所有 token 的 Key 和 Value 向量，因此节省了内存使用。

### **注意事项**

- KV Cache 需要额外的内存来存储 Key 和 Value 向量，因此在处理非常长的序列时，可能会占用较大的内存空间。
- 由于 KV Cache 依赖于之前生成的 token，如果序列中出现重复的 token，它们的 Key 和 Value 向量会有所不同，因此 KV Cache 是针对特定序列生成过程的优化。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YmUyYTJjOTNmN2M5ODIyYzg2MDljNWNhMmFhYTg0ZjdfV1l2TmlldGdGRjlRejl0QmZhZEIxdVdhQVd0ZXhpTDFfVG9rZW46TGsyMGJMTWs2b3locjd4M2xKYWNRVjJabkFmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 2、并行

### 数据并行（DP）

https://zhuanlan.zhihu.com/p/617133971

数据并行的核心思想是：在各个GPU上都拷贝一份完整模型，各自吃一份数据，算一份梯度，最后对梯度进行累加来更新整体模型。理念不复杂，但到了大模型场景，巨大的存储和GPU间的通讯量，就是系统设计要考虑的重点了。在本文中，我们将递进介绍三种主流数据并行的实现方式：

- DP（Data Parallelism）：最早的数据并行模式，一般采用参数服务器(Parameters Server)这一编程框架。实际中多用于单机多卡
- DDP（Distributed Data Parallelism）：分布式数据并行，采用Ring AllReduce的通讯方式，实际中多用于多机场景
- ZeRO：零冗余优化器。由微软推出并应用于其DeepSpeed框架中。严格来讲ZeRO采用数据并行+张量并行的方式，旨在降低存储。

### DP：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTE1Y2ExYTFhZDhhODViZDFhZDU1MDBmMmFlNTgxMDFfUWpmZUZwQVI5SjRUZXE3VmNkWFVRc2lOV05kWkQ5YWlfVG9rZW46RUJmVGJ1aHc5b2dsY0d4c25mUWNRdmd0bmRiXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

PS架构

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWJlYjk3OGI3MDAxYmY3OGRhMDU2Y2FjZWY4OGEyODZfdm1IRnk4NlIxb2VBM1hFenY5OHFxYmllM3R6SzR2ZG1fVG9rZW46SllNc2JNS29rb0pNNjd4S0ZLWGNnanhQbk5nXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

问题：

- 存储开销大。每块GPU上都存了一份完整的模型，造成冗余。关于这一点的优化，我们将在后文ZeRO部分做讲解。
- 通讯开销大。Server需要和每一个Worker进行梯度传输。当Server和Worker不在一台机器上时，Server的带宽将会成为整个系统的计算效率瓶颈。

### DDP：

采用Ring All reduce

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTQ0NjU5MGU4YmMwZjc2NzIwZDEyZjlkMDBhOTBjNzBfTlFYa3I4TnNveW4zN3E5TElNNEU4U2tSMXVRYXplcG5fVG9rZW46SHFQcGJMSlRRbzRUUHh4bDA4cWNzUFdFbnBjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MzdkNTExMjRiOTVkOWE4NjgxZTIwYWI3OTVlZWEzODlfWkRaSWptdjBMc1pOYlNnSHJjd1YwZUJzeUo5cjZyOHJfVG9rZW46UEhlYWJ1aDNNbzVpb3l4Tk5ZNWNtU29Dbm1NXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=Njg5NDkzZDAyOWNmZGE4MTk4OGIzNDFlMmNkNTU5ZjlfRmtXN0xWbk5LQVhzSzBaNHB5MHBoa0xkZWtkMWR4amlfVG9rZW46VFZaTmJPeGJybzhQaXZ4eGd3cmNxcEhvbkpnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

以此类推，同样经过3轮迭代后，使得每块GPU上都汇总到了完整的数据

总结：

1、在DP中，每个GPU上都拷贝一份完整的模型，每个GPU上处理batch的一部分数据，所有GPU算出来的梯度进行累加后，再传回各GPU用于更新参数

2、DP多采用参数服务器这一编程框架，一般由若个计算Worker和1个梯度聚合Server组成。Server与每个Worker通讯，Worker间并不通讯。因此Server承担了系统所有的通讯压力。基于此DP常用于单机多卡场景。

3、异步梯度更新是提升计算通讯比的一种方法，延迟更新的步数大小决定了模型的收敛速度。

4、Ring-AllReduce通过定义网络环拓扑的方式，将通讯压力均衡地分到每个GPU上，使得跨机器的数据并行（DDP）得以高效实现。

5、DP和DDP的总通讯量相同，但因负载不均的原因，DP需要耗费更多的时间搬运数据

### Zero:

https://zhuanlan.zhihu.com/p/618865052

### 张量并行

https://zhuanlan.zhihu.com/p/622212228

## 3、注意力优化

### 多头注意力、多查询、分组查询

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YTk0ZmRiNzgyMGMxZWE0MGY1ZmU5MGRkZTI0ODI0MjRfNDliNE1XdFczdjdNM2VTVER3aGt3dE1CVUFKUGtlVWJfVG9rZW46Q0FNRGIwZmVjb1huZ3J4cXZIYmNVUFFwbnljXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWZmNjcyNzAyNGY5MjE1MmRjZjY1NzhhNzY5NzNhYzZfNnBlbnh6SmFoVjVibTlNN1hETUVGb1h3TVVqVkx1bEpfVG9rZW46WG41ZWJqNjJSb2syU2F4aHJFMmN3MGlObjBnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 4、FlashAttention

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=OTAxZjgxNDg0NDRkOGY3MmVjZjc3Yzk3ZmRkMWU5MzhfeWJLTFpDU2dJTmhMQ3o4WmE0SEFzUkdZc2R2a1M4ZHpfVG9rZW46S2x2TGJwTXJtb2k5cER4bFhZR2NGNzAwbm5jXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

https://zhuanlan.zhihu.com/p/639228219

Flash Attention通过调整注意力的计算顺序，引入两个额外的统计量进行分块计算，避免了实例化完整的 N×N 的注意力矩阵 P,S ，将显存复杂度从 O(N2) 降低到了 O(N) 。另外，对于内存受限的标准注意力，Flash Attention通过kernel融合和分块计算，大量减少了HBM访问次数，尽管由于后向传递中的重计算增加了额外的计算量FLOPs，减少了运行时间，计算速度更快（GPT2的7.6倍）。

## 5、PagedAttention

https://zhuanlan.zhihu.com/p/638468472

https://blog.vllm.ai/2023/06/20/vllm.html

PagedAttention 原理（一）

用于自回归生成的 KV cache 占大量显存，受OS中的虚拟内存和分页的思想启发，提出了该 attention 优化算法，可在不连续的显存空间存储连续的 key 和 value。用于将每个序列的 KV cache 分块（blocks），每块包含固定数量的 token 的 key 和 value 张量。

因为 blocks 在显存中不必连续，所以可以像 OS 的虚拟内存分页一样，以更灵活的方式管理键和值：

将 block 视为 page

将 token 视为 bytes

将序列视为进程

序列的连续逻辑块通过 block table 映射到非连续物理块。

物理块可在生成新 token 时按需分配。因此只有最后一个block会发生显存浪费，小于4%。

PagedAttention 原理（二）

并行采样时，同一个 prompt 生成多个输出序列，这些序列生成时可以共享 prompt 的 attention 计算和显存。

与 OS 中进程共享物理 page 的方式类似，不同序列可以通过将其逻辑块映射到同一物理块来共享块。为了确保共享安全，Paged Attention 跟踪物理块的引用计数，并实现 “写时复制”（Copy-on-Write）机制，即需要修改时才复制块副本。内存共享使得显存占用减少 55%，吞吐量提升 2.2x。

## 6、模型压缩技术

### 6.1 模型量化

参考https://blog.csdn.net/qq_25295605/article/details/141951407

#### 量化概念

量化是大模型领域中的一项关键技术，它通过降低模型参数的精度，将浮点数转换为整数或[定点数](https://so.csdn.net/so/search?q=定点数&spm=1001.2101.3001.7020)，从而实现模型的压缩和优化。这样做的主要目的是减少模型的存储需求、加快推理速度，并降低模型的计算复杂度，使得大模型能够更高效地在资源受限的设备上运行，例如移动设备、嵌入式系统等场景。

#### 精度概念

bit 位是计算机中最小的数据单位，只能存储 0 或 1 两种状态。一个 bit 可以表示两种状态，即 0 或 1；

byte 字节是计算机中常用的数据单位，由 8 个 bit 组成；

float 浮点数是一种用于表示实数的数据类型，通常由 32 位或 64 位的二进制数表示，其中 32 位的浮点数称为单精度浮点数，64 位的浮点数称为双精度浮点数；

integer 整数是一种用于表示整数的数据类型，通常由 8 位、16 位、32 位或 64 位的二进制数表示，其中 8 位的整数称为字节，16 位的整数称为短整数，32 位的整数称为整数，64 位的整数称为长整数；

1. **FP32（单精度浮点数）**

- **结构**：32 位（1 位符号 + 8 位指数 + 23 位尾数）
- **特点**：
  - **高精度**：适合科学计算和模型训练，能准确表示小数值。
  - **大范围**：指数范围约为 10−3810−38 到 10381038。
- **用途**：
  - 传统深度学习训练（如 TensorFlow/PyTorch 的默认类型）。
  - 需要高精度的数值模拟（如物理仿真）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTI3YmM2M2JhMDU1NDg5OGU2OTVjNmFjMzRiMWNjNjNfNVFja1I0dmtFYUFPWDMxUGptazhQeDk1UGV2SloxRDBfVG9rZW46T1JoNWJVRnVBb2RLVEZ4MjRZbmNWbFpXbnVoXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

1. **FP16（半精度浮点数）**

- **结构**：16 位（1 位符号 + 5 位指数 + 10 位尾数）
- **特点**：
  - **内存减半**：相比 FP32，内存占用减少 50%。
  - **精度有限**：尾数位少，易导致数值溢出（如梯度消失/爆炸）。
- **用途**：
  - 训练中的混合精度计算（与 FP32 结合使用）。
  - 边缘设备推理（如 NVIDIA Jetson）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=YjExMDRmNjg4ZWIwYTY0MzI4ZWZkMDJkYjFjYmRkMzFfcVZxSEhlU1JUd0l1SnNrak5EeEFZRFJvRGdEYnkyamtfVG9rZW46VFZwTmJLWDNnb1BScmt4emJ0S2NhaElkbm9nXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

1. **BF16（Brain Floating Point 16）**

- **结构**：16 位（1 位符号 + 8 位指数 + 7 位尾数）
- **特点**：
  - **动态范围大**：指数位与 FP32 对齐（范围相同），但尾数精度低。
  - **兼容性**：适合从 FP32 转换，减少训练中的数值不稳定。
- **用途**：
  - 大模型训练（如 GPT-3、BERT）。
  - 需要大范围的数值计算（如强化学习）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmViZmExZmJlYzg5NzAyMGJjYmJmOWVmMDc0NzJlN2FfdDJnYXNPbXAxdUdiZjJYaWkzVUh6Z1pSWkxKc1UxelVfVG9rZW46T2h4bWIxN0xvb1hzcWV4M3IzSmNJcGlTbjRmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

1. **INT8（8 位整数）**

- **结构**：8 位（无符号：0~255；有符号：-128~127）
- **特点**：
  - **低内存**：内存占用仅为 FP32 的 1/4。
  - **量化损失**：需通过校准（Calibration）减少精度损失。
- **用途**：
  - 模型推理加速（如 TensorRT 量化）。
  - 移动端部署（如手机、摄像头）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NjhjYjExYWI1MDViZGI3MzVjMGNiZTZhMTM5Y2RiNmRfWHdkSTUwZjhCdFZudTFibEU5dWZVNFh3ZGg4MWRncW1fVG9rZW46TlluRWI1NmxVb2JaSXV4UFY3M2M0SlowbklmXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 量化核心原理

量化通过缩放因子（scale）和零点（zero point）将浮点数映射到整数范围：

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ODMyZmE1ZWY5YTU0YWRhNDRlYjcxMzBjZjE1ZTIxNjFfQ1RsZW93V08wQ1o5dkJDMnRlSk9OOWVrdWNkNkNHNTFfVG9rZW46WXJyQmJqRm1Cb25hV2x4M2JwaWNLb3R0bmNkXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MjgyMWZmMWYxMjRlZTI0ZDg5YTI0MWQxNjFiZDAwYzJfcUdVTmoxc2Y5VnVZRmZlQ2kxUGh3eUYxNUpYREREa1hfVG9rZW46TlJuU2JvaXBhb01DWWR4Z1k0aWNRVGNCbkhnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### 量化粒度

Per-tensor：整个张量或整个层级共享相同的量化参数（scale和zero-point）。这种方式的优点是存储和计算效率较高，但可能会导致精度损失，因为一个固定的量化参数难以覆盖所有数据的动态范围;

Per-channel：每个通道或每个轴都有自己的量化参数。这种方式可以更准确地量化数据，因为每个通道可以有自己的动态范围，但会增加存储需求和计算复杂度;

Per-group：在量化过程中，将数据分成块或组，每块或每组有自己的量化参数。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjI4NTlhYTliNjFkODA4YWEyM2NmZWUxYjRjZTdkZThfVW9pWXJYNTBBYlV2TTZvRjljZDFuYkJtZlNrRkdxYWZfVG9rZW46U1l5WWJXdzdDb2NrVU54V202aGM4dGp3bnZlXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### PTQ和QAT

量化感知训练（QAT）通过在模型训练阶段模拟量化操作，使模型适应低精度计算，从而减少推理时的精度损失。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=M2YzM2FiYWFlYTI3YmQ1ZGJlOTc3YThmZTJkNTQzZmFfRjlmSEV4cVdKV2k5aDlTZ011T2F5NFVpTHREUXFIU1ZfVG9rZW46SmdhdGJTT1ZWb3VxdnV4cVBSR2NsdHF1bjRaXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

伪量化操作与实际量化操作的区别详解

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=M2FkYzdlN2IwZTZkNDAwZDM0NDE3M2U3ODA3ZTRjYjBfWnJHN0QxcVFqVDNLYUxHS3hJNENLcUh0ZjVzRTdWN3BfVG9rZW46SFJaR2J1SExXbzllUHZ4YTRjc2NEcEpTbjVjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NGNhNTRlNWVlYjE1NWFmMWRjM2Y5ODYwMmRiYjBhODJfR2VWanFVR0xTZmJGMkFtQ1RxRXVzR1hORmlJbUtZVkdfVG9rZW46UFBMdGJZaVBMb1ZJb1h4djQyU2NXamUzbkUwXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

1. **训练后量化（PTQ）概述**

训练后量化（Post-Training Quantization, PTQ）是一种在模型训练完成后对模型进行量化的方法，无需重新训练模型。其核心思想是将模型的权重和激活值从高精度（如 FP32）转换为低精度（如 INT8），从而减少模型的存储空间和计算复杂度，同时尽量保持模型的精度。

1. **PTQ 的主要方法**

PTQ 主要分为两种方法：动态量化和静态量化。

**2.1 动态量化（Dynamic Quantization）**

- **定义**：动态量化仅将模型中特定算子的权重从 FP32 类型映射成 INT8/16 类型，而激活值在运行阶段才进行量化。这意味着对于不同的输入值，其缩放因子是动态计算的。
- **优点**：
  - **实现简单**：只需要量化权重，激活值在推理时动态量化。
  - **模型精度影响小**：权重量化成 INT16 类型时，模型精度基本不受影响；权重量化成 INT8 类型时，模型精度会受到一定影响，但模型大小显著减小。
- **缺点**：
  - **性能较差**：由于激活值在推理时动态量化，计算开销较大，性能不如静态量化。
- **应用场景**：适用于对模型精度要求较高，但对推理速度要求不高的场景。

**2.2 静态量化（Static Quantization）**

- **定义**：静态量化也称为校正量化或数据集量化，使用少量无标签校准数据。其核心是计算量化比例因子，使用静态量化后的模型进行预测，在此过程中量化模型的缩放因子会根据输入数据的分布进行调整。
- **优点**：
  - **精度更高**：通过校准数据调整量化参数，能够更好地适应输入数据的分布，减少量化误差，提高模型精度。
  - **计算效率高**：量化参数在模型转换阶段确定，推理时不需要动态计算，计算效率较高。
- **缺点**：
  - **实现复杂**：需要计算和存储每个通道的量化参数，增加了计算开销。
  - **存储需求增加**：每个通道需要独立的量化参数，会增加模型的存储需求。
- **应用场景**：适用于需要高精度和高推理速度的场景，特别是在卷积神经网络中。

1. **PTQ 的具体实现**

**3.1 动态量化实现**

动态量化通常用于权重量化，激活值在推理时动态量化。以下是一个简单的实现步骤：

1. **量化权重**：将模型中特定算子的权重从 FP32 类型量化成 INT8/16 类型。
2. **推理时动态量化激活值**：在推理过程中，根据输入数据动态计算激活值的量化参数。

**3.2 静态量化实现**

静态量化需要使用校准数据来计算量化参数。以下是一个简单的实现步骤：

1. **准备校准数据**：使用少量无标签数据作为校准数据。
2. **计算量化参数**：通过校准数据计算量化比例因子。
3. **量化模型**：使用计算得到的量化参数对模型进行量化。
4. **推理**：使用量化后的模型进行推理。

#### **LLM.int8()**

**一、LLM.int8() 的背景**

传统量化方法（如 INT8 量化）在小型模型上表现良好，但在大规模语言模型（如 GPT、BERT）中会导致显著的精度损失，主要原因包括：

1. **离群值问题**：LLMs 中存在一些极端大的激活值（outliers），导致量化范围不合理。
2. **逐层误差累积**：量化误差在深层模型中逐层传播并放大。
3. **分布复杂性**：LLMs 的权重和激活值分布复杂，难以用简单的对称量化或非对称量化描述。

LLM.int8() 的提出正是为了解决这些问题。

**二、LLM.int8() 的核心思想**

LLM.int8() 的两大核心技术是：

1. **分块量化（Block-wise Quantization）**：将矩阵按块（block）划分，每块单独量化，降低离群值影响。
2. **离群值分离（Outlier Separation）**：将极端大的激活值分离出来，用 FP16 处理，其余部分用 INT8 处理。

**三、LLM.int8() 的详细流程**

1. **矩阵分块**

- 将输入矩阵（如激活值或权重矩阵）划分为多个小块（block），每块大小为 （例如 2048×4096 的矩阵可划分为多个 128×128 的块）。
- 每块独立进行量化，确保离群值的影响被限制在局部范围内。

1. **离群值检测**

- 对每个块统计激活值的分布，检测是否存在离群值（通常定义为超出某个阈值，如 3 倍标准差）。
- 如果存在离群值，将离群值单独提取并用 FP16 处理，其余值用 INT8 处理。

1. **混合精度计算**

- **INT8 部分**：对非离群值使用标准 INT8 量化，包括量化和反量化操作。

```Plain
q = round(w / s)       # 量化
w' = q * s             # 反量化
```

- **FP16 部分**：对离群值保留 FP16 精度，避免精度损失。

1. **矩阵乘法优化**

- 使用分块矩阵乘法（block-wise matrix multiplication），将 INT8 和 FP16 部分分开计算，最后将结果相加。

**四、LLM.int8() 的优势**

1. **高精度**：通过离群值分离和分块量化，极大降低了量化误差，精度损失几乎可忽略（在 BLOOM 和 GPT 模型上，准确率仅下降 0.1%）。
2. **高效性**：显著减少显存占用（最高可减少 4 倍）和计算开销，适合 GPU 推理和训练。
3. **通用性**：支持所有基于 Transformer 的大规模语言模型（如 GPT、BERT、BLOOM 等），且无需微调或重新训练。

**五、LLM.int8() 的局限性**

1. **计算复杂度**：离群值分离和混合精度计算增加了部分计算开销，但相比显存节省和速度提升，代价可接受。
2. **硬件支持**：依赖高效的 INT8/FP16 混合计算硬件（如 NVIDIA GPU），在低端设备上优化效果有限。
3. **训练阶段支持**：主要针对推理优化，训练阶段的量化需要额外研究

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWExYWNjZWRiZWFiZDEzMWI0ZGM3YWFlODhmZjdlZTNfa0kxV0tmdEQ0anR2dm5Pa0pUZGNnSXhzQkNSWUhiZU1fVG9rZW46Q0dsc2JPOVM1b2YyWE94TzdVdmM0VU8zblBnXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

#### GPTQ

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MTUzYjllNDc3OTg1ZDdiZWNkM2MzOTNhN2QzNTJkZGJfZUVVZzBlMFo1QU53UW1YbUZ4N2ZNaVR4bEJGZEc3MVFfVG9rZW46WUVUMGJWRWR4b09la094UTBzVmM2TE9MbjViXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

在 Transformers 中使用 GPTQ 只需提前安装AutoGPTQ和[Optimum](https://link.zhihu.com/?target=https%3A//github.com/huggingface/optimum)即可，使用 GPTQ 方法量化transformer模型具体示例如下：

```Python
from transformers import AutoModelForCausalLM, AutoTokenizer, GPTQConfig

model_id = "facebook/opt-125m"
tokenizer = AutoTokenizer.from_pretrained(model_id)
quantization_config = GPTQConfig(bits=4, dataset = "c4", tokenizer=tokenizer)

model = AutoModelForCausalLM.from_pretrained(model_id, device_map="auto", quantization_config=quantization_config)
```

#### **SmoothQuant** 

详见https://www.zhihu.com/question/576376372/answer/3388402085

**背景**

在大规模语言模型中，量化面临的主要挑战是**激活值的极端分布**（即存在大量离群值），这会导致：

1. **量化范围不合理**：传统的对称量化或非对称量化无法有效覆盖激活值的动态范围。
2. **精度损失严重**：离群值的存在会显著放大量化误差，尤其是在深层模型中。

SmoothQuant 的核心目标是通过对激活值和权重的联合优化，解决这一难题，实现高效的 INT8 量

**SmoothQuant 的核心思想**

SmoothQuant 的核心技术是**激活平滑（Activation Smoothing）**，通过引入一个平滑因子（smoothing factor）对激活值进行缩放，使其分布更加均匀，从而更适合量化。具体步骤如下：

1. **激活值平滑**：对整个激活张量进行平滑处理，减少离群值的影响。
2. **权重量化**：对权重进行量化，同时调整量化参数以补偿激活值的平滑缩放。
3. **联合优化**：通过优化平滑因子和量化参数，最小化量化误差。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=N2JlYjEyYWZkNmJhMmM3NDRkNzJhMDQ4MzFhYjE3MzBfNmxZVDdlVW9KTVcyRjcxcHZiOEJBeW9KWTZUd2pNa0pfVG9rZW46U1BGdWJ2dmFObzZaWlR4eTRvY2NKOW92bk1KXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

**SmoothQuant 的优势**

1. **高精度**：通过激活平滑和联合优化，显著降低量化误差，在 BLOOM 和 GPT 模型上，精度损失几乎可忽略。
2. **高效性**：支持 INT8 量化，显著减少显存占用和计算开销。
3. **通用性**：支持所有基于 Transformer 的大规模语言模型（如 GPT、BERT、BLOOM 等），且无需微调或重新训练。

**SmoothQuant 的局限性**

1. **计算复杂度**：激活平滑和联合优化增加了部分计算开销，但相比显存节省和速度提升，代价可接受。
2. **硬件支持**：依赖高效的 INT8 计算硬件（如 NVIDIA GPU），在低端设备上优化效果有限。
3. **训练阶段支持**：主要针对推理优化，训练阶段的量化需要额外研究。

和LLM.int8()对比

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=NWNmNTU2ZDFmN2JlNDQwZjhlNzBhMmMyNTE1Nzk3ZTBfOFJQS2FNTmdnMUNpbVJ0RWVDY0FFbXpVUWlBdnpWc3BfVG9rZW46R01Ta2JjSWRab05WZUx4dFRzVWN0bTdlbkhDXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

AWQ、SPQR等等其他的量化方法原理介绍可以参考https://www.zhihu.com/question/627484732/answer/3261671478

### 6.2 模型剪枝

#### **模型剪枝（Model Pruning）详解**

https://zhuanlan.zhihu.com/p/692858636?

1. **背景**

模型剪枝是一种通过**减少模型参数和计算量**来压缩模型大小的技术，同时尽可能保持模型的性能。在大规模深度学习模型中（如 Transformer 架构）中，模型剪枝可以显著减少显存占用和计算开销，提升模型的部署效率和推理速度。

1. **模型剪枝的核心思想**

模型剪枝的核心是通过**移除不重要的参数或结构**，减少模型的复杂度。剪枝的目标是：

- **减少参数量**：降低模型大小。
- **减少计算量**：提升推理速度。
- **保持性能**：尽可能减少精度损失。

1. **模型剪枝的分类**

根据剪枝的粒度，可分为以下三类：

1. **非结构化剪枝（Unstructured Pruning）**：
   1. 逐个剪掉不重要的权重（如设置为 0）。
   2. 优点：灵活，可以移除任何不重要的权重。
   3. 缺点：稀疏矩阵计算效率低，硬件难以加速。
2. **结构化剪枝（Structured Pruning）**：
   1. 移除整个神经元、滤波器或层。
   2. 优点：生成的模型仍是密集矩阵，硬件支持好。
   3. 缺点：灵活性较低，可能带来较大的精度损失。

1. **模型剪枝的流程**

模型剪枝的一般流程包括：

1. **训练一个基准模型**。
2. **评估参数重要性**：
   1. 使用准则（如权重绝对值、梯度、重要性评分）评估每个参数的重要性。
3. **剪枝**：
   1. 根据重要性移除不重要的参数或结构。
4. **微调**：
   1. 对剪枝后的模型进行微调，恢复性能。
5. **迭代**：
   1. 重复上述步骤，直到达到目标压缩率或性能。

1. **剪枝重要性的评估准则**

以下是一些常用准则：

- **权重绝对值**：移除绝对值较小的权重。
- **梯度值**：移除对损失函数影响较小的权重。
- **重要性评分**：通过启发式方法（如 L1/L2 范数）评估权重重要性。

1. **剪枝在 Transformer 架构中的应用**

Transformer 模型（如 BERT、GPT 等）由于其大规模参数和计算量，特别适合剪枝。以下是剪枝在 Transformer 中的具体应用：

**6.1. Attention 头的剪枝**

- **方法**：移除不重要的注意力头（Attention Head）。
- **准则**：基于注意力头的贡献度（如输出权重的 L2 范数）评估重要性。
- **优点**：直接减少多头注意力机制的计算量。
- **示例**：在 BERT 中，移除 30% 的注意力头，精度损失可控制在 1% 以内。

**6.2. 权重矩阵的剪枝**

- **方法**：对权重矩阵（如 Q、K、V 矩阵或全连接层权重）进行稀疏剪枝。
- **准则**：基于权重绝对值或重要性评分移除不重要的参数。
- **优点**：显著减少矩阵乘法的计算量。
- **示例**：在 GPT 中，对全连接层进行 50% 的稀疏剪枝，推理速度提升 2 倍。

**6.3. 层的剪枝**

- **方法**：移除不重要的 Transformer 层。
- **准则**：基于层对输出的贡献度评估重要性。
- **优点**：直接减少模型的深度和显存占用。
- **示例**：在 BERT 中，移除 4 层（共 12 层），精度损失可控制在 2% 以内。

**6.4. 嵌入层的剪枝**

- **方法**：对词嵌入（Embedding）矩阵进行剪枝。
- **准则**：基于词频或重要性评分移除不常用的词向量。
- **优点**：减少词嵌入的显存占用。

1. **剪枝的挑战**

- **精度损失**：剪枝可能带来精度下降，尤其在极端情况下。
- **硬件支持**：非结构化剪枝生成的稀疏矩阵难以加速，需要专用硬件支持。
- **迭代成本**：剪枝和微调需要多次迭代，时间成本较高。

1. **剪枝与其他压缩技术的结合**

剪枝通常与其他模型压缩技术（如量化、知识蒸馏）结合使用，以进一步提升压缩效果：

- **剪枝 + 量化**：先剪枝减少参数量，再量化减少位宽。
- **剪枝 + 知识蒸馏**：通过教师模型指导剪枝后的学生模型恢复性能。

#### **主流大模型剪枝方案详解**

大模型（如GPT、LLaMA、PaLM等）因其庞大的参数量和计算需求，剪枝技术需要更精细的策略以平衡压缩率与性能保留。以下是当前主流的几种大模型剪枝方案及其核心技术：

##### **1. 结构化剪枝：LLM-Pruner（微软）**

- **核心思想**： 针对Transformer架构的大模型，通过移除冗余的注意力头（Attention Heads）、中间层维度（Feed-Forward Network宽度）或整个层（Layers），实现结构化压缩。
- **关键技术**：
  - **重要性评分**：使用权重范数（如L2）或梯度敏感度评估模块重要性。
  - **依赖感知剪枝**：考虑模块间的依赖关系（如残差连接），避免因剪枝导致特征传递断裂。
  - **轻量级恢复**：剪枝后仅需少量数据（1-5%训练集）微调即可恢复性能。
- **效果**：
  - 在LLaMA-7B上移除20%参数，精度损失小于2%。
  - 支持硬件友好加速（无需稀疏计算库）。
- **代码示例**：

```Python
# 伪代码：移除低重要性注意力头
importance_scores = [head.norm() for head in attention_heads]
sorted_indices = np.argsort(importance_scores)
pruned_heads = sorted_indices[:num_heads_to_prune]
model.prune_heads(pruned_heads)
```

##### **2. 非结构化剪枝：SparseGPT（一次性剪枝）**

- **核心思想**： 直接对预训练大模型进行非结构化剪枝，无需微调，通过近似优化最小化剪枝后的输出误差。
- **关键技术**：
  - **逐层贪心剪枝**：按层顺序剪枝，每次剪枝后修正剩余权重以补偿误差。
  - **Hessian矩阵近似**：利用权重二阶导数（Hessian）信息指导重要性评估，避免迭代优化。
  - **分组剪枝**：将权重分组（如每行一组），组内按重要性移除部分参数。
- **效果**：
  - 在OPT-175B上剪枝50%权重，零样本任务精度下降小于5%。
  - 支持4位量化与剪枝联合压缩。
- **适用场景**：
  - 资源受限无法微调的场景（如云端大模型即时部署）。

##### **3. 动态剪枝：Wanda（权重与激活联合剪枝）**

- **核心思想**： 基于权重与激活值的乘积（Weight-Activation Product）评估参数重要性，动态决定剪枝目标。
- **公式**： 对权重 W和输入激活 A，重要性评分为 ∣Wi,j∣⋅∥Aj∥2，移除低评分权重。
- **优势**：
  - 更贴近实际推理过程，保留对输出影响大的参数。
  - 在相同压缩率下，比传统L1剪枝精度更高。
- **实验效果**：
  - 在LLaMA系列模型上，剪枝30%权重，精度损失可忽略。

##### **4. 混合专家剪枝（MoE Pruning）**

- **适用模型**： 针对混合专家模型（如Switch Transformer、Mixtral），剪枝冗余的专家（Experts）。
- **策略**：
  - **专家重要性评估**：根据专家被调用的频率或输出贡献度排序。
  - **门控网络优化**：调整门控（Gating）函数，减少低价值专家的激活概率。
  - **渐进式剪枝**：逐步移除最少使用的专家，并微调剩余专家。
- **效果**：
  - 在Switch-Base-64上剪枝50%专家，任务精度保持98%以上。

##### **5. 稀疏训练与剪枝结合：LoRAPrune**

- **核心思想**： 在低秩适配（LoRA）微调过程中引入稀疏性，逐步剪枝冗余参数。
- **步骤**：
  - 使用LoRA为模型添加低秩适配层。
  - 在微调过程中，通过梯度下降自动稀疏化LoRA参数。
  - 移除稀疏化的LoRA权重，恢复原始模型结构。
- **优势**：
  - 无需额外剪枝算法，微调过程自动完成压缩。
  - 支持大模型的高效参数更新（仅训练LoRA部分）。

**技术对比与选择建议**

| 方案        | 剪枝类型 | 是否需要微调 | 硬件友好性     | 适用场景                   |
| ----------- | -------- | ------------ | -------------- | -------------------------- |
| LLM-Pruner  | 结构化   | 少量数据微调 | 高             | 需要明确结构压缩的部署场景 |
| SparseGPT   | 非结构化 | 无需微调     | 低（需稀疏库） | 即时压缩预训练模型         |
| Wanda       | 非结构化 | 可选微调     | 低             | 高精度保留的通用剪枝       |
| MoE Pruning | 结构化   | 需要微调     | 高             | 专家模型优化               |
| LoRAPrune   | 混合     | 微调中完成   | 中             | 结合适配器的高效压缩       |

**实践建议**

1. **从结构化剪枝入手**： 若需快速部署，优先选择LLM-Pruner或MoE剪枝，因其对硬件兼容性更好。
2. **非结构化剪枝的高效利用**： 使用SparseGPT或Wanda时，搭配NVIDIA的Sparse Tensor Core可提升推理速度。
3. **联合压缩技术**： 剪枝后进一步应用量化（如GPTQ），模型体积可再减少50-70%。

### 6.3 知识蒸馏

#### 核心原理

**定义**：通过训练小模型（学生）模仿大模型（教师）的输出分布和内部特征，传递隐含知识（Dark Knowledge）。 **提出背景**：2015年Hinton团队首次系统提出（《Distilling the Knowledge in a Neural Network》），核心突破在于使用软标签（Soft Target）替代硬标签（Hard Label）。

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=MzNkZDgxYzU4NGZkOTIyNWE1MzMwNDFmZjVmMzZiY2JfemRMRWlNeDBhekVJM2NoTVpFdHlZTmFZckZZeVVyQUZfVG9rZW46QXFyc2JBUlQwb3RIT0V4NDBSZWM5aTFxbkdjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

看个例子理解知识蒸馏：

#### 例子：知识蒸馏就像 **学霸教学渣**

**场景设定**： ▸ **学霸（教师模型）**：能考95分的大学霸，但解题速度慢 ▸ **学渣（学生模型）**：只能考70分，但做题非常快

现在我们想让学渣解题能力接近学霸，但保持速度优势。

关键步骤解析（以数学考试为例）：

1. **普通教学法 （传统训练）** 📖 老师直接给答案： 问题："2+3×4=?" 标准答案是14 ❌ 学渣只记住答案，不理解过程

**缺点**：做题只会生搬硬套，碰到"3+2×5"仍然不会

1. **知识蒸馏教学法** 🧑🏫 学霸示范解题思路： ▸ "先乘后加"的规则（规则知识） ▸ 强调容易出错点："不要先加2+3"（错误模式） ▸ 近似问题："如果是2×(3+4)，答案又不同"（关系推理）

**效果**：即使遇到新题型"4+5×3"，学渣也能举一反三

对应到AI技术中的要素：

| 现实教学   | 技术对应           | 数学表达（简版）                  |
| ---------- | ------------------ | --------------------------------- |
| 标准答案   | 真实标签（硬标签） | y = [0, 1, 0] （直接答案）        |
| 学霸的思路 | 软标签             | y' = [0.1, 0.7, 0.2] （概率分布） |
| 错误分析   | 温度参数调节       | T=3时，0.7→0.5，突出差异          |

技术流程的具象化步骤

**实例：手写数字识别（区分数字3和8）**

1. 
   1. "顶部弯曲较大可能是8"（特征提取）
   2. "底部闭合更可能是3"（关键判定点）
   3. 给出概率：[3: 30%，8: 70%] （软标签）
2. **学渣（学生模型）的学习**：
   1. 不仅记住最终答案
   2. 模仿思考："虽然像3，但顶部这个弧度更像8"（特征关注）
   3. 调整自己的判断逻辑
3. **学习效果对比**：

| 方法     | 识别正确率 | 模型大小 | 推理速度 |
| -------- | ---------- | -------- | -------- |
| 自学     | 75%        | 小       | 快速     |
| 普通教学 | 82%        | 小       | 快速     |
| 知识蒸馏 | 89%        | 小       | 快速     |
| 学霸本人 | 96%        | 大       | 慢       |

为什么需要「温度参数」？

继续用考试做类比： ▸ **高温（T=10）**：学霸会说："这道题像30%的3、70%的8，但也有0.1%可能是9"（平滑分布） ▸ **低温（T=1）**：学霸直接说："这就是8！"（非黑即白）

**科学验证**：在ImageNet数据集上，使用T=3相比T=1，学生模型准确率提升约2.3%

一句话总结

知识蒸馏就是 **让小模型通过模仿大模型的"思考方式"，而不是死记硬背答案**，最终达到既轻量又聪明的效果。

#### 例子：用PyTorch实现BERT-base（110M参数）模型蒸馏

```Python
# 定义师生模型
from transformers import BertForSequenceClassification, BertConfig
# 教师模型（BERT-base 110M参数）
teacher = BertForSequenceClassification.from_pretrained('bert-base-uncased')

# 学生模型配置（层数减半）
student_config = BertConfig(
    hidden_size=768,
    num_hidden_layers=6,  # 原BERT-base为12层
    num_attention_heads=12,
    intermediate_size=3072,
    num_labels=2  # 假设是二分类任务
)
student = BertForSequenceClassification(student_config) 

print(f"教师参数量: {teacher.num_parameters()/1e6:.1f}M")  # 110.1M
print(f"学生参数量: {student.num_parameters()/1e6:.1f}M")   # 37.3M
# 定义蒸馏损失函数
import torch.nn as nn
import torch.nn.functional as F
class DistillLoss(nn.Module):
    def __init__(self, alpha=0.5, temperature=2.0):
        super().__init__()
        self.alpha = alpha
        self.temperature = temperature
        
    def forward(self, student_logits, teacher_logits, labels):
        # 知识蒸馏损失（软化后的KL损失）
        soft_teacher = F.softmax(teacher_logits / self.temperature, dim=-1)
        soft_student = F.log_softmax(student_logits / self.temperature, dim=-1)
        kld_loss = F.kl_div(soft_student, soft_teacher, reduction="batchmean") * (self.temperature ** 2)
        
        # 常规交叉熵损失
        ce_loss = F.cross_entropy(student_logits, labels)
        
        return self.alpha * kld_loss + (1 - self.alpha) * ce_loss

from transformers import AdamW, get_linear_schedule_with_warmup
from datasets import load_dataset
from torch.utils.data import DataLoader
from transformers import BertTokenizer

# 超参数配置
BATCH_SIZE = 16
EPOCHS = 3
LR = 5e-5
WARMUP_STEPS = 100

# 1. 数据预处理
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')

def preprocess(examples):
    return tokenizer(
        examples['text'],
        truncation=True,
        padding='max_length',
        max_length=256,
        return_tensors='pt'
    )

# 使用部分IMDB数据集示例
dataset = load_dataset("imdb")
train_dataset = dataset["train"].select(range(1000)).map(preprocess, batched=True)
eval_dataset = dataset["test"].select(range(200)).map(preprocess, batched=True)

# 转换为PyTorch DataLoader
train_loader = DataLoader(train_dataset, batch_size=BATCH_SIZE, shuffle=True)
eval_loader = DataLoader(eval_dataset, batch_size=BATCH_SIZE)

# 2. 训练准备
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
teacher.to(device)
student.to(device)

optimizer = AdamW(student.parameters(), lr=LR)
total_steps = len(train_loader) * EPOCHS
scheduler = get_linear_schedule_with_warmup(optimizer, WARMUP_STEPS, total_steps)
criterion = DistillLoss(alpha=0.7, temperature=2.0)

# 3. 训练循环
for epoch in range(EPOCHS):
    # 训练阶段
    teacher.eval()
    student.train()
    total_loss = 0
    
    for batch in train_loader:
        inputs = {k: v.to(device) for k, v in batch.items() if k != 'text'}
        labels = inputs['labels']
        
        # 教师预测（不计算梯度）
        with torch.no_grad():
            teacher_outputs = teacher(**inputs)
        
        # 学生预测
        student_outputs = student(**inputs)
        
        # 计算蒸馏损失
        loss = criterion(
            student_outputs.logits,
            teacher_outputs.logits,
            labels
        )
        
        # 反向传播
        loss.backward()
        optimizer.step()
        scheduler.step()
        optimizer.zero_grad()
        
        total_loss += loss.item()
    
    # 评估阶段
    student.eval()
    correct = 0
    total = 0
    
    with torch.no_grad():
        for batch in eval_loader:
            inputs = {k: v.to(device) for k, v in batch.items() if k != 'text'}
            labels = inputs['labels']
            
            outputs = student(**inputs)
            preds = torch.argmax(outputs.logits, dim=1)
            correct += (preds == labels).sum().item()
            total += labels.size(0)
    
    print(f"Epoch {epoch+1}/{EPOCHS}")
    print(f"Train Loss: {total_loss/len(train_loader):.4f}")
    print(f"Val Acc: {correct/total:.2%}\n")

# 保存最终模型
torch.save(student.state_dict(), "distilled_bert.pth")
```

## 7、模型服务技术

### 动态批处理(Continuous Batching)

https://zhuanlan.zhihu.com/p/676109470

https://zhuanlan.zhihu.com/p/652165071

### 投机采样

https://zhuanlan.zhihu.com/p/651359908

![img](https://a5kgk6ph1i.feishu.cn/space/api/box/stream/download/asynccode/?code=N2UzNWI4N2VkNmQwMDM1OGJhYzc2ZTk3YWRmY2QyN2NfQ2JsVWZqQ09GRGphdFZZcmtvUXBLMWF4NXNLNWU4UDVfVG9rZW46WWZjUWJaRWx1b2pZQ2J4SkkwN2NCMFd3bkFjXzE3MzkwMDE2MDc6MTczOTAwNTIwN19WNA)

## 8、矩阵乘优化

https://zhuanlan.zhihu.com/p/435908830

https://zhuanlan.zhihu.com/p/442930482

## 9、推理框架总结

https://zhuanlan.zhihu.com/p/653352979

https://blog.csdn.net/qq_27590277/article/details/133759166

### Vllm

https://www.processon.com/diagraming/640558bf1c8923293d848a44

### llama.cpp

`llama.cpp` 是一个基于 C++ 实现的大型语言模型（LLM）推理工具。根据搜索结果，以下是 `llama.cpp` 使用的一些技术来加速推理过程：

1. **量化推理**：`llama.cpp` 支持量化推理，可以将模型参数从浮点数转换为低比特的整型，如8位整数，从而减少模型大小和内存占用，加快推理速度734。
2. **底层计算优化**：通过优化底层计算和内存管理，`llama.cpp` 可以在不牺牲模型性能的前提下提高推理速度7。
3. **硬件高效利用**：`llama.cpp` 对硬件进行了高效利用，支持多种设备和操作系统。对于 Windows/Linux 用户，推荐与 BLAS（或 cuBLAS 如果有 GPU）一起编译，可以显著提升 prompt 处理速度。对于 macOS 用户，由于已对 ARM NEON 做优化，并且已自动启用 BLAS，无需额外操作3。
4. **多设备支持**：`llama.cpp` 支持在多种硬件上运行，包括 CPU 和 GPU，利用不同硬件的特性来加速推理过程3。
5. **模型剪枝**：虽然搜索结果中没有直接提到 `llama.cpp` 使用模型剪枝技术，但这是一个常见的推理加速技术，通过去除模型中的冗余参数来减少推理时间4。
6. **并行计算**：使用并行计算技术，如 GPU 加速，可以显著提升模型的推理速度，尽管搜索结果中没有明确提到 `llama.cpp` 使用此技术，但考虑到它是大型模型推理工具，这可能是一个潜在的加速手段。
7. **API 接口优化**：`llama.cpp` 提供了丰富的 API 接口，方便开发者在自己的项目中集成 LLM 推理功能，这可能涉及到对 API 进行优化以提高效率2。

### Tgi

1、张量并行

2、量化

3、flash attention和paged attention

4、投机采样

5、continuous batching

https://zhuanlan.zhihu.com/p/675292919

### tensorrt

https://zhuanlan.zhihu.com/p/371239130

参考文献：

1、https://s3tlxskbq3.feishu.cn/docx/NyPqdCKraoXz9gxNVCfcIFdnnAc

2、https://transformers.run/c1/attention/

3、https://github.com/liguodongiot/llm-action/tree/main

4、https://blog.csdn.net/qq_25295605/article/details/141951407
