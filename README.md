__在代码中都有许多注释，一些API的功能和参数都做好了标注,每一步的输入输出维度也有说明，可以放心食用__



# 词嵌入

项目代码：  [查看代码](word_embedding.ipynb)

设计下游任务为电影评论分类，获取Embedding层的词向量，然后获得指定单词前10相似的单词

从结果来看，使用此训练并不能太好的理解词义，可能是训练集也不是很大，然后这个任务也不是很适合理解词义（可能使用skip-gram模型或者CBOW模型在配合维基百科语料库更好做这个任务），仅仅训练了10个周期,最终结果可能也和embedding层的随机初始化有关。

当然，在这一个过程中，对于词嵌入还是有了更多的理解。

### 运行结果

本地训练，Embedding_size=50,epoch=10,最相似的10个单词

> wonderful-->['wonderful', 'everyone', 'haunting','underrated', 'brilliant', 'fantastic', 'High', 'superb','marvel','recommended']

colab上，embedding_size=300,epoch=10，最相似的10个单词

> womderful-->['wonderful', 'haunting', 'everyone', 'brilliant', 'marvel', 'fantastic', 'underrated', 'superb', 'perfect', 'flaw']



鉴于效果一般，之后在下载了Glove50词嵌入文件

根据词嵌入向量的余弦相似度计算相似的单词：

a to b like c to __ 例如:

- man to women like king to quuen
- Paris to France like Beijing to China

### 运行结果

```
man-->woman like boy --> girl
small-->smaller like large --> larger
italy-->italian like china --> chinese
Japan-->Tokyo like China --> taipei (怕不是要杀头 ORZ)
```



# RNN文本分类

项目代码：[查看代码](使用RNN进行文本分类.ipynb)

使用循环神经网络完成IMDB电影评论分类（positive or negative）

最终对自己输入的影评进行打分（0-1）

最终训练结果如下：

```
comment is: this movie is bad. but the actor is very handsome and I like him. but I will not recommend this movie.
here is the point: 0.17458665
```

```
comment is: The movie was cool. The animation and the graphics were out of this world. I would recommend this movie.
here is the point:0.9981263
```

```
comment is: actually, I am the actor's fans. But his performance in the movie break my heart.
here is the point:0.47038242
```

```
comment is: The characters is not famous, but their performances make the movie reach a very high level! 
here is the point:0.9868593
```

```
comment is: The movie is very ironic.This film criticizes the social phenomena without conscience
here is the point:0.99971634
```

# 恐龙名字生成

项目代码：[查看代码](恐龙名字文本生成.ipynb)

此项目是莎士比亚风格文本生成的基础版本。通过这个项目可以对于后面的项目有更好的把握

加载语料库/dions.txt中众多恐龙名字作为训练预料，最后产生一个可以生成恐龙风格名字的模型。

## 运行结果

```
未训练：
njywwtcmeqodygspv
Dga
Sa
Dodygspv
Qjvfekyneazagqvaaxund
15个周期后：
Saousos
Xtruromos
Sairraurusn
Hurusn
Sndhlurdaybgos
```

# 莎士比亚风格文本生成

项目代码：[查看代码](莎士比亚风格文本生成.ipynb)

对莎士比亚的作品学习，给定起始字符（下方运行结果中，给定的起始单词为'ROMEO: '）,训练出来的模型将会自动生成莎士比亚风格类型的文本。

### 运行结果：

> ROMEO:
> 
> I advance fiture each other,  
>How many haughty love, your own suspicion from so rounder he divide,  
> As if I had some all fell.   
> 
> Fullow:  
> Bleased the soldiers, Cleome,  
> And thou hadst beat me back to Man.  
>In an outward stars that sle with thee?  
> Why should she noble endary?    
> 
> .............



# 注意力模型-日期翻译

项目代码：[查看代码](/date_translation.ipynb)

了解Attention：[关于Attention的不错文章](https://zhuanlan.zhihu.com/p/37601161)

实现一个简单版本的注意力模型，实践这个之后再做下一个机器翻译项目更佳。对于给定的不同类型日期格式，翻译为标准格式YYYY-MM-DD

最终对于大部分格式的日期都能准确翻译，但对于xx/xx/xxxx这类型的数据处理不太好。

## 运行结果

```
source: 3/may/1979
output: 1999-05-33

source: 18.4.2009
output: 2009-04-18

source: 04 22 2004
output: 2004-04-22

source: 6th of August 2016
output: 2016-08-06

source: Tue 10 Jul 2020
output: 2000-07-10

source: March 4 2009
output: 2009-03-04

source: 12/23/2001
output: 2010-12-21

source: monday march 7 2013
output: 2013-03-07

```

# 注意力模型-机器翻译

项目代码：[查看代码](注意力机制-机器翻译.ipynb)

了解Attention：[关于Attention的不错文章](https://zhuanlan.zhihu.com/p/37601161)



基于Bahdanau注意力模型，论文中底层使用双向RNN（这里使用的单向GRU）。 

为了便于训练，我只使用了30000条较短的数据（西班牙语--->英语），对于较短句子（10个单词以内）翻译效果还行。

若想获得更好的效果，可以使用更多的语料(num_samples=None)，在colab上训练更多的周期。







# Transformer模型

项目代码：[查看代码](./Transformer模型.ipynb)

训练了一个Transformer模型。将葡萄牙语翻译为英语。

了解Transformer：[关于Transformer的不错文章](https://blog.csdn.net/qq_41664845/article/details/84969266)

项目使用数据集来自于 [TED 演讲开放翻译项目](https://www.ted.com/participate/translate)，该数据集包含来约 50000 条训练样本，1100 条验证样本，以及 2000 条测试样本。
