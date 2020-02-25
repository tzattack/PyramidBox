人脸检测模块 仲耀晖

## 安装环境
* Ubuntu 16.04 LTS
* Python3
* Tensorflow-gpu 1.4
* OpenCV3

## 当前模型效果（数据集为 WIDER FACE 的验证集）:

| Method | AP Easy | AP Medium | AP Hard |
|:-------|:-------:|:-------:|:-------:
| **当前模型** | **90.6** | **88.8** | **73.4** |

## 运行方法
```
python demo.py
```

### 模型训练方法
1. 下载 [VGG 16 模型](https://github.com/tensorflow/models/tree/master/research/slim) 并将其放置于 /checkpoints.  
2. 下载 [WIDER FACE 数据集](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/) 并转换为 VOC 格式. 路径格式为:
```
datasets/
       |->widerface/
       |    |->WIDER_train/
       |    |->WIDER_val/
       |    |->WIDER_test/
       |    |->Annotations/
       |    |->JPEGImages/
       |    |...
```
3. 使用这个命令来将数据转为 tfrecord 格式的数据:
```
python datasets/pascalvoc_to_tfrecords.py
```
4. 训练策略分为两步:
先将 `train_model.py` 中的设置改为如下设置再运行，用来训练 PyramidBox 的额外网络层:
```
self.fine_tune_vgg16 = False
```
5. 然后设置 `self.fine_tune_vgg16 =Ture` 并运行 `train_model.py` 来训练整个网络.  

### 测试
使用以下脚本进行测试：  
```
python widerface_eval.py
cd eval/eval_tools
octave wider_eval.m
```

## 引用

[SSD-Tensorflow](https://github.com/balancap/SSD-Tensorflow)<br>
[SSD_tensorflow_VOC](https://github.com/LevinJ/SSD_tensorflow_VOC)

