# 3d-gaussian-splatting
## 项目概述

本项目实现基于 3D Gaussian Splatting 技术的物体三维重建与新视图合成，通过拍摄物体多角度图像，利用 COLMAP 进行相机标定，再训练 3D Gaussian 模型实现高质量的三维场景表示与视图渲染。

## 项目结构

```
3d-gaussian-splatting/
├── data/                  # 存放拍摄的图片和处理后的数据
├── gaussian-splatting/    # 3d-gaussian-splatting代码库
└── output/                # 模型输出文件
```

## 快速开始

### 1. 数据采集

#### 拍摄准备
- 拍摄物体的多角度图片
- 将拍摄的图片放入 `data/xxx/input` 文件夹

### 2. 环境配置

1. 安装COLMAP
```bash
conda install -c conda-forge colmap
```
2. 安装 gaussian-splatting 及其依赖库
```bash
git clone https://github.com/graphdeco-inria/gaussian-splatting --recursive
conda env create --file gaussian-splatting/environment.yml
conda activate gaussian_splatting
pip install tensorboard
```

3. COLMAP 估计相机参数
```bash
python gaussian-splatting/convert.py -s data/cat
```
   


### 3. 模型训练与评估

#### 启动训练
```bash
python gaussian-splatting/train.py -s data/cat --eval
```

#### 模型评估
```bash
python gaussian-splatting/metrics.py -m output/8210f869-3
```
模型和评估结果文件存储在output文件中。
最终测试集上结果为：
- SSIM :    0.8789158
- PSNR :   22.6018848
- LPIPS:    0.3465531

模型下载：https://pan.baidu.com/s/17MdFS4hdaTHqddjLjedeSQ?pwd=kyzx
重建视频：https://pan.baidu.com/s/1SzltqwvfzOzN14o0Vwt_sw?pwd=ub4p
