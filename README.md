# industry-mouse-detect
工业环境老鼠检测

![Python 3.7](https://img.shields.io/badge/python-3.7-green.svg?style=plastic)
![Pytorch 1.0.0](https://img.shields.io/badge/pytorch-1.0.0-green.svg?style=plastic)
![cuDNN 7.3.1](https://img.shields.io/badge/cudnn-7.3.1-green.svg?style=plastic)
![License CC BY-NC](https://img.shields.io/badge/license-CC_BY--NC-green.svg?style=plastic)

## 背景介绍
本工程着重识别工业环境中的老鼠，以便能够得到及时、有效的处理。本工程的难度如下：
- 老鼠与背景色难以区分
- 老鼠经常出没在晚上，增加识别难度
- 老鼠体型较小，传统的图像处理方法和神经网络方法难以识别 
- 工业环境要求较高的处理速度，一般的神经网络方法难以满足
## 实现方法简介
鉴于本项目天然的难度，采用单一手段无法处理，现使用复合方法：
1. 采用YOLOV3-darknet为backbone的主干神经网络结构，以残差方减小梯度消失（YOLOV3拥有20+的FPS，能够满足高性能的工业需求）
2. 采用双帧差分监测帧与帧之间像素级别变化，并改动网络结构做重点监督训练（解决夜晚识别效果差问题、解决老鼠天然保护色问题）
3. 修改主干网络先验框尺寸，方便小物体能得到充分的学习（解决小物体检测问题）

主干网络结构如下：
<div align=left>
  <img width=200 height=250 src="https://github.com/yangbisheng2009/industry-mouse-detect/blob/master/image/yolo-struct.jpg" >
</div>

## 模型线上效果展示
## 如何使用本项目
```shell
#train
python train.py --backbone darknet --epochs 90 --batch-size 16 --checkpoint ./checkpoint --data-dir ./data

#test
python test.py

#predict
python predict.py --model darknet --checkpoint ./checkpoint/x
```
## 感谢
