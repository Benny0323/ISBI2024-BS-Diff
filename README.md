# BS-Diff: Effective Bone Suppression in CXRs via Conditional Diffusion Models

![](https://img.shields.io/badge/-Github-181717?style=flat-square&logo=Github&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Awesome-FC60A8?style=flat-square&logo=Awesome&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=Python&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Pytorch-EE4C2C?style=flat-square&logo=Pytorch&logoColor=FFFFFF)

<div align=center><img width="500" height="500" src="https://github.com/Benny0323/BS-Diff/assets/104205136/e8edb3b0-559d-4a61-90ac-9a6ea53e7a4e)"/></div>

## Proposed method 

We spend a lot of time collecting and summarizing relevant papers and datasets, where you can find them at https://github.com/diaoquesang/Diffusion_model-based_bone_suppression_in_chest_X-rays

This code is a pytorch implementation of our paper "BS-Diff: Effective Bone Suppression in CXRs via Conditional Diffusion Models", which is **under review by ISBI2024**.

Our proposed framework comprises two stages: **a conditional diffusion model (CDM) equipped with a U-Net architecture and a simple enhancement module** that incorporates an autoencoder. It can not only generate soft tissue images with **a high bone suppression ratio** but also possess the capability to **capture fine image information and spatial features,
while preserving overall structures**. The image below shows our proposed network.

![image](https://github.com/Benny0323/BS/blob/main/framework.png)

## The bone-suppressed images generated by our method
![image](https://github.com/Benny0323/BS/blob/main/contrast.png)

## Comparison performance with previous works (visualization)
![image](https://github.com/Benny0323/BS/blob/main/Comparison.png)
## Pre-requisties
* Linux

* Python>=3.7

* NVIDIA GPU (memory>=5G) + CUDA cuDNN

### Download the dataset
Now, we only provide three paired images with CXRs and soft-tissues. Soon, we will make them available to the public after data usage permission. Theree paired images are located at
```
├─ BS
│    ├─ 0.png
│    ├─ 1.png
│    └─ 2.png
├─ CXR
│    ├─ 0.png
│    ├─ 1.png
│    └─ 2.png
```
## Getting started to evaluate
### Install dependencies
```
pip install -r requirements.txt
```
### Download the checkpoint
Due to the fact that our proposed model comprises two stages, you need to download both stages' checkpoints to successfully run the codes!
```
├─ Stage1
│    ├─ Aug_Final_ctrain.pth
└─ Stage2
     ├─ Aug_Hybrid_autoencoderkl.pth
```
### Evaluation
To do the evaluation process, first run the following command of stage 1 (the conditional diffusion model):
```
python Test.py
```      
Then, you will get a series of images generated by the conditional diffusion model. After that, run the following command of stage 2 with these images as inputs.
```
python Aug_Hybrid_autoencoderkleval.py
```
## Train by yourself
If you want to train our model by yourself, you can run the following command of stage 1:
```
python Train.py
```
Then after finishing stage 1, you can use the generated output of stage 1 to train our stage (enhancement module) by running the following command:
```
python Hybridloss_autoencoderkl.py
```
These two files are located at
```
├─ Stage1
│    └─ Train.py
└─ Stage2
     ├─ Hybridloss_autoencoderkl.py
     └─ pytorch_msssim.py
```
**Attention: the file 'pytorch_ssim.py' should be used during training in stage 2. So do not delete it!**

## Evaluation metrics
You can also run the following commands about evaluation metrics in our experiment incuding PSNR, SSIM, MSE and BSR:
```
python metrics.py
```      
