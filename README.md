---

本模型为 Decoder-only，参数为200M 预训练模型，基于 Pytorch 框架，训练数据为现有开源数据集mobvoi_seq_monkey_general_open_corpus通用数据集和BelleGroup对话数据集，取其中部分数据作为训练集

> 注：本模型仅仅是以学习为目的
>

## 模型下载
可以使用如下方式下载模型

```bash
#安装ModelScope
pip install modelscope
```

```python
#SDK模型下载
from modelscope import snapshot_download
model_dir = snapshot_download('lzklllzzz/SLM_200M_SFT')
```

或者访问魔塔的lzklllzzz/SLM_200M_SFT 目录即可

## 依赖下载使用
python 3.10

```bash
pip install -r requirements.txt
```

## 下载所需数据集
```bash
bash data_process/data_download.sh
```

数据会被下载到当前目录的 train_data文件夹

## 数据预处理
```bash
python data_process/data_preprocess.sh
```

## tokenizer训练
bpe训练方式，这个过程比较占用内存，所以采用通用数据集的100万条数据进行训练，词表大小为6144

```bash
python train_tokenizer.py
```

接下来是对模型的预训练和微调

## 预训练
```bash
python train/pretrain.py
```

## 微调
```bash
python train/sft_full.py
```

## 测试
```bash
python pretrain_sample.py
python sft_sample.py
```



此模型为学习目的，资源有限，所以预训练和微调仅仅只用了部分数据集，所需显卡也只有一张4090

预训练用时 10h

微调   12h

tokenizer 以及训练的模型已开源：[https://www.modelscope.cn/models/lzklllzzz/SLM_200M_SFT](https://www.modelscope.cn/models/lzklllzzz/SLM_200M_SFT)  


