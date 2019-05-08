## Introduction

本仓库专注于 Bert  在文本分类领域的应用， 探索在 Bert 之上如何提高文本分类上的表现。

## Requirements

- Pytorch
- 

## 数据集

仓库采用了三个数据集，分别是 SST-2 情感分类， Yelp多标签分类， THUCNews 多标签分类。 

其中，  [THUCNews](http://thuctc.thunlp.org/)  只选取了一个子集， 该子集中包括了10个分类，每个分类6500条数据：
> - train： 5000 * 10
> - dev: 500 * 10
> - test： 1000 * 10

## 关于 Bert 

这里，使用了 [pytorch-pretrained-BERT](https://github.com/huggingface/pytorch-pretrained-BERT) 来加载 Bert 模型， 考虑到国内网速问题，推荐先将相关的 Bert 文件下载，主要有两种文件：
> - vocab.txt: 记录了Bert中所用词表
> - 模型参数： 主要包括预训练模型的相关参数

相关文件下载连接在 [Bert](./Bert.md)

## 实验设置

- 本实验均在单1080ti上运行，但并没有删除在单机多卡上的逻辑，只是删除了分布式运算的逻辑，主要是考虑到大多数实验大家都没有必要去用到分布式。
- 删除了采用 fp16 的逻辑， 考虑到文本分类所需的资源并没有那么大， 采用 默认的32位浮点类型也是可以的。
- **注意**： Bert 的参数量随着文本长度的增加呈现接近线性变化的趋势， 而 THUCNews 数据集的文本长度大多在1000-4000之间，这对于大多数机器是不可承受的， 测试在单1080ti上， 文本长度设置为150左右已经是极限。


## Results

### THUCNews

model_name | ACC | F1 | Loss 
--- |--- | --- | --- 
BertOrigin | | |

### SST-2

```

```

| model_name | Acc  | F1   | Loss |      |
| ---------- | ---- | ---- | ---- | ---- |
| BertOrigin |      |      |      |      |
|            |      |      |      |      |


### Yelp



## 如何适配自己的数据集

如果你想要适配自己的数据集，你只需要添加一个Processor即可， 推荐先将数据转化为 tsv 格式， 这是因为仓库本身实现了对 tsv 文件的支持， 毕竟转化逻辑要比重新一个新的读取逻辑更加简单。