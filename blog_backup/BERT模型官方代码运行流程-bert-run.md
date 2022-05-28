### BERT模型官方代码运行流程

BERT源码地址：https://github.com/google-research/bert

#### 准备

1. clone项目代码

地址：https://github.com/google-research/bert.git

2. 下载预训练好的模型与数据集

![image-20211003223453081](https://blog.caowei.xyz/blog/dl-4.png)

![image-20211002165902304](https://blog.caowei.xyz/blog/dl-1.png)

3. 将模型放在项目中或项目外（后面参数配置会用到两者的**相对路径**）

![image-20211003223122326](https://blog.caowei.xyz/blog/dl-3.png)

3. 在PyCharm中配置运行参数及参数说明（以分类任务为例）

````shell
#任务名
--task_name=MRPC
\
#是否训练
--do_train=true
\
#是否验证
--do_eval=true
\
#数据集路径
--data_dir=GLUE/glue_data/MRPC
\
#语料库
--vocab_file=GLUE/BERT_BASE_DIR/uncased_L-12_H-768_A-12/vocab.txt
#配置文件
--bert_config_file=GLUE/BERT_BASE_DIR/uncased_L-12_H-768_A-12/bert_config.json
\
#预训练好的模型
--init_checkpoint=GLUE/BERT_BASE_DIR/uncased_L-12_H-768_A-12/bert_model.ckpt
\
#最大字数/字母数
--max_seq_length=128
\
#每次训练所抓取的数据样本数量
--train_batch_size=32
\
#学习率
--learning_rate=2e-5
\
#训练迭代次数
--num_train_epochs=3.0
\
#结果保存位置
--output_dir=GLUE/out
````

![image-20211003222912358](https://blog.caowei.xyz/blog/dl-2.png)

#### 运行`run_classifier.py`

结果如图：

![image-20211003223714703](https://blog.caowei.xyz/blog/dl-5.png)