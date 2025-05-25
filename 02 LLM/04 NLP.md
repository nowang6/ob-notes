

# 知识图谱


https://github.com/husthuke/awesome-knowledge-graph


# Schema

![[Pasted image 20240611085143.png]]

![[Pasted image 20240611085338.png]]
![[Pasted image 20240611085620.png]]

# 数据集

实体抽取：ontonotes
事件抽取： ACE


开源项目
https://github.com/yanqiangmiffy?tab=stars

网站

模型推理






https://modelscope.cn/models/ZJUNLP/OneKE/summary


![[Pasted image 20240610200911.png]]


# 困惑度（Perplexity)

计算困惑度

```python
import torch
from transformers import BertTokenizer, GPT2LMHeadModel

model_path = "uer/gpt2-chinese-cluecorpussmall"
tokenizer = BertTokenizer.from_pretrained(model_path)
model = GPT2LMHeadModel.from_pretrained(model_path)


sentences = ["今天是个好日子。", "天今子日。个是好", "这个婴儿有900000克呢。", "我不会忘记和你一起奋斗的时光。",
"我不会记忘和你一起奋斗的时光。", "会我记忘和你斗起一奋的时光。"]

inputs = tokenizer(sentences, padding='max_length', max_length=50, truncation=True, return_tensors="pt")

outputs = model(**inputs, labels=inputs['input_ids'])
logits = outputs["logits"]

# 错位构造logits和label
# 后续可用于计算交叉熵损失
shift_logits = logits[:, :-1, :].contiguous()
shift_labels = inputs['input_ids'][:, 1:].contiguous()
shift_attentions = inputs['attention_mask'][:, 1:].contiguous()

# reshape成(bs*sl, vocab_size)
loss_fct = CrossEntropyLoss(ignore_index=0, reduction="none")
loss = loss_fct(shift_logits.view(-1, shift_logits.size(-1)), shift_labels.view(-1)).detach().reshape(bs, -1)

ppls = torch.exp(meanloss).numpy().tolist()
for sentence, ppl in zip(sentences, ppls):
	print('"{}"这句话的困惑度为: {}'.format(sentence, ppl))

```


# 相似度

计算MinHash相似度
```python
from datasketch import MinHash, MinHashLSH
import jieba
import re

query = "有些鸟儿是永远关不住的,因为它们的每一片羽翼上都沾满了自由的光辉。"
sentences = [
"有些鸟儿是永远不会被关在牢笼里的，因为它们的每一片羽毛都闪耀着自由的光辉。",
"这世上到处都是害怕主动迈出第一步的孤独之人。"
]
regex = re.compile('，|。')
def split_word(sentence):
	global regex
	return [word for word in jieba.lcut(re.sub(regex, ' ',sentence)) if word.strip()]

query_lcut = split_word(query)
sentences_lcut = [split_word(sentence) for sentence in sentences]

实例化LSH管理器
# threshold=0.5，指Jaccard相似度阈值设置为0.5，即返回大于0.5的待匹配句子
# num_perm=128，指Hash置换函数的个数，如需提高精度可适当提高，如256
threshold = 0.5
num_perm=128
lsh = MinHashLSH(threshold=threshold, num_perm=num_perm)
for idx, sentence_lcut in enumerate(sentences_lcut):
# 对每个待匹配句子实例化1个MinHash()对象
	minhash = MinHash()

# 将文本的词序列传入MinHash对象

	minhash.update_batch([word.encode('utf-8') for word in sentence_lcut])

# 将MinHash对象传入LSH对象进行管理

	lsh.insert("minhash_sentence_{}".format(idx+1), minhash)

# query语句也需要进行MinHash实例化
minhash_query = MinHash()

minhash_query.update_batch([word.encode('utf-8') for word in query_lcut])
# 调用LSH实例的query方法对之前传入的待匹配句子进行相似文本匹配

simi_result = lsh.query(minhash_query)

print("近似Jaccard相似度>{}的句子有：\n{}".format(threshold, simi_result))

# 调用LSH实例的remove方法删除其中存有的文本，传入参数为相应文本的key

lsh.remove('minhash_sentence_1')

# 调用LSH实例的keys属性，查看目前存有的文本的key

list(lsh.keys)
```

# 对比学习
ConSERT
SimCSE


# BERT

## 二个阶段
BERT整体框架包含**pre-train**和**fine-tune**两个阶段
pre-train阶段模型是在无标注的标签数据上进行训练，fine-tune阶段，BERT模型首先是被pre-train模型参数初始化，然后所有的参数会用下游的有标注的数据进行训练
## Embedding

- **Token Embeddings**是词向量，第一个单词是CLS标志，可以用于之后的分类任务
- **Segment Embeddings**用来区别两种句子，因为预训练不光做LM还要做以两个句子为输入的分类任务
- **Position Embeddings**和之前文章中的Transformer不一样，不是三角函数而是学习出来的


## pre-train的2个任务
MLM：Mask Language Model
Next Sentence Prediction（NSP）


## ALBERT 轻量级BERT

ALBERT针对BERT的修改主要有两点，

- **嵌入参数化进行因式分解**
- **跨层参数共享**
- **NSP任务更改为SOP任务**,  句子顺序预测

## RoBERT
训练时间更长，batch size更大，数据更多
删除了 NSP
动态MASK

![[Pasted image 20240106170104.png]]
The key differences introduced by RoBERTa are:
- Removing the next sentence prediction task from pre-training (binary-classification task of predicting whether two sentences are a pair from the same text).
- Using dynamic masking instead of static masking.




