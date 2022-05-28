### 项目地址

https://github.com/649453932/Bert-Chinese-Text-Classification-Pytorch

### 数据集

[THUCNews](http://thuctc.thunlp.org/)

抽取了20万条新闻标题，文本长度在20到30之间。

一共10个类别，每类2万条。

数据以字为单位输入模型。

数据集划分：

| 数据集 | 数据量 |
| :----: | :----: |
| 训练集 |  18万  |
| 测试集 |  1万   |
| 验证集 |  1万   |

### 项目环境

+ python 3.7
+ pytorch > 1.1
+ tqdm
+ sklearn
+ tensorboardX

### 项目运行

#### 数据准备

1. 下载bert_Chinese模型

https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese.tar.gz

2. 下载词表

https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese-vocab.txt

3. 将bert模型与词表放在bert_pretain目录下，目录中应包含三个文件：

+ pytorch_model.bin
+ bert_config.json
+ vocab.txt

#### 训练并测试

```shell
python run.py --model bert
```

#### 遇到的问题与解决方法

1. FileNotFoundError

![image-20211006190004163](https://blog.caowei.xyz/blog/dl-10.png)

解决方法：

在对应目录下创建`saved_dict`文件夹。

再次运行，问题解决：

![image-20211006193526018](https://blog.caowei.xyz/blog/dl-11.png)

#### 运行结果

![image-20211007212122878](https://blog.caowei.xyz/blog/dl-13.png)