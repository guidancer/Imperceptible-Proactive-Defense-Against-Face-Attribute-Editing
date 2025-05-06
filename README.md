# 不可感知的人脸属性编辑主动防御

![Python 3.10](https://img.shields.io/badge/python-3.10-green.svg?style=plastic)

![PyTorch 1.13.1](https://img.shields.io/badge/pytorch-1.13.1-green.svg?style=plastic)


> **摘要:** *尽管基于生成对抗网络(GAN)的人脸属性编辑主动防御方法比基于梯度攻击的方法具有更快的对抗扰动生成速度，但现有这类方法仍未能很好平衡主动防御性能与生成扰动的不可感知性。因此，本文基于GAN提出了一种不可感知的人脸属性编辑主动防御方法。为了增强生成扰动的不可感知性，该方法设计了一种高频信息补偿机制以促使生成器生成更多人眼更不敏感的高频扰动。为了提升生成扰动的主动防御性能，该方法设计了一种多级密集连接机制以减少编码过程中的语义损失。同时，该方法在训练中引入人脸显著性对抗损失，使扰动能更好地破坏人脸伪造区域。本文在单个模型和跨模型防御场景下分别进行了实验。结果表明，所提方法相比现有主动防御方法能生成不可感知性更强的对抗扰动，且对目标模型取得较高的防御成功率。*


## 数据集与预训练模型

数据集使用CelebA数据集,具体下载可参考[CMUA-Watermark](https://github.com/VDIGPKU/CMUA-Watermark). 

人脸属性编辑模型StarGAN、AttentionGAN、AttGAN、FGAN的预训练权重与本文训练的U2Net的预训练权重及自建数据集均可从百度网盘进行下载,并相应修改settings.json中的路径配置微数据集解压后的具体存储路径.

点击([Pretrained Weights](https://pan.baidu.com/s/1AMhVnrcB4OIUOwym8tP7eA?pwd=msch))下载本文方法涉及的预训练权重,按照路径存放相应的权重.

```xml
AttentionGAN路径：'./AttentionGAN/AttentionGAN_v1_multi/checkpoints/celeba_256_pretrained/'
AttGAN路径：'./AttGAN/output/256_shortcut1_inject0_none/checkpoint/'
FGAN路径：'./fgan/ckpts/'
StarGAN路径：'./stargan/stargan_celeba_256/models/'
U2Net路径：'./face_sod_u2net/ckpts/'
```

点击([Face-SOD-DataSet](https://pan.baidu.com/s/1f-SRP5J-9OEs4TFNT4_10w?pwd=r33j))下载本文自建人脸显著性数据集,包含了12000张训练集图片与3000张测试集图片,可用于训练各种显著性检测模型用于检测人脸显著性区域任务.


## 训练
执行下列命令以训练模型对AttGAN进行攻击

```python
  python -m train_sfgan.att_sod_loss
```
执行下列命令以训练模型对AttentionGAN进行攻击

```python
  python -m train_sfgan.attention_sod_loss
```
执行下列命令以训练模型对FGAN进行攻击

```python
  python -m train_sfgan.fgan_sod_loss
```
执行下列命令以训练模型进行集成攻击

```python
  python -m train_sfgan.ensemble
```

## 预训练权重
跨模型防御场景下的权重为easy_ensemble.pth，以供想要使用这一项目的开发者进行测试。

## 相关工作
本工作部分基于 [CMUA-Watermark](https://github.com/VDIGPKU/CMUA-Watermark) 、 [WaveGAN](https://github.com/kobeshegu/ECCV2022_WaveGAN) 、 [DenseNet](https://github.com/bamos/densenet.pytorch)、[U2Net](https://github.com/xuebinqin/U-2-Net)和[Fixed-Point-GAN
](https://github.com/mahfuzmohammad/Fixed-Point-GAN).感谢他们高质量的工作.

有任何相关问题均可以联系：fyf200613@qq.com或者202212490275@nuist.edu.cn
