# 一、Bert原始预训练模型
1. 几个特点：
- 利用了MLM(Masked Language Model)架构，从而能实现双向语言模型的训练
- 是双任务预训练，预测masked token和预测next sentence
- 既能用于sentence级别的任务，也能用于token级别的任务
- 通常，额外加一层输出层，即可微调特定任务
- bert输出，每个位置输出一个大小为 hidden_ size 的向量，同时输出
# 二、适用下游任务
句子级别：
- 文本分类

token级别：
- NER
# 三、Bert生态
不同的bert，训练语料是不同的。在做任务时，需要根据不同bert的特性，选择合适的bert作为backbone。
| Bert      | Description |
| ----------- | ----------- |
| chinese-roberta-wwm-ext      | 如果是中文文本，优选       |
| deberta-v3-base   | 如果是英文文本，优选        | 
| finbert   | 如果是金融领域，优选        | 
| xxx-large-bert   | 如果算力足，优选        | 
# 四、Bert微调方法
Bert底部的层，学到的是通用语义信息，比如词性、词法等语言学知识，而靠近顶部的层，会倾向于学习到接近下游任务的知识，拿预训练任务来说，就是masked word prediction和next sentence prediction任务中的知识。
1. 全参数微调
2. 使用权重初始化

finetune时，可以保留底部的bert权重，对于顶部层的权重，可以重新进行随机初始化，让这部分参数在你的任务上进行重新学习。

3. 冻结部分参数微调
