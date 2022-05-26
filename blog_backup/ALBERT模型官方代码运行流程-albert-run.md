 ALBERT源码地址：https://github.com/google-research/albert

#### 准备

1. clone项目代码

地址：https://github.com/google-research/albert.git

2. 下载预训练好的模型与数据集（以GLUE为例）

![image-20211004161127625](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/dl-4)

GLUE数据集下载地址：[GLUE Benchmark](https://gluebenchmark.com/tasks)

3. 将模型放在项目中或项目外（后面参数配置会用到两者的**相对路径**）

![image-20211004162538161](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/dl-6.png)

![image-20211004162901991](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/dl-7.png)

3. 在PyCharm中配置运行参数及参数说明（以基于MRPC数据集的分类任务为例）

````shell
#数据集路径
--data_dir=GLUE/glue_data
\
#结果保存位置
--output_dir=GLUE/output
\
#预训练好的模型
--init_checkpoint=GLUE/albert_base/model.ckpt-best
\
#配置文件
--albert_config_file=GLUE/albert_base/albert_config.json
\
#是否训练
--do_train=true
\
#是否验证
--do_eval=true
\
#是否预测
--do_predict=true
\
#是否区分大小写，当值为true时，则忽略大小写
--do_lower_case=true
\
#每一条训练数据（两句话）相加后的最大长度限制
--max_seq_length=128
\
#指定优化器
--optimizer=adamw
\
#任务名
--task_name=MRPC
\
#预热次数
--warmup_step=1000
\
#分词模型
--spm_model_file=GLUE/albert_base/30k-clean.model
\
#学习率
--learning_rate=3e-5
\
#训练轮数
--train_step=10000
\
#每多少轮保存一次权重
--save_checkpoints_steps=100
\
#batch size 设置主要看经验。
#5000样本数据集可以设置在32，1w以上数据集可以设置128。以此类推.....
--train_batch_size=128
````

![image-20211004163304766](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/dl-8.png)

#### 运行`run_classifier.py`

![image-20211004195020026](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/dl-9.png)


