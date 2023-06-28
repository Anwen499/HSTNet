# HSTNet for remote sensing image super-resolution
Official Pytorch implementation of the paper "[Hybrid-Scale Hierarchical Transformer for Remote Sensing Image Super-Resolution].

Super-resolution (SR) technology plays a crucial role in improving the spatial resolution of remote sensing images so as to overcome the physical limitations of spaceborne imaging systems. Although deep convolutional neural networks have achieved promising results, most of them overlook the advantage of self-similarity information across different scales and high-dimensional features after the upsampling layers. To address the problem, we propose a hybrid-scale hierarchical transformer network~(HSTNet) to achieve faithful remote sensing image SR. Specifically, we propose a hybrid-scale feature exploitation module to leverage the internal recursive information in single and cross scales within the images. To fully leverage the high-dimensional features and enhance discrimination, we design a cross-scale enhancement transformer to capture long-range dependencies and efficiently calculate the relevance between high-dimension and low-dimension features. The proposed HSTNet achieves the best result in PSNR and SSIM on UCMecred dataset and AID dataset. Comparative experiments demonstrate the effectiveness of the proposed methods and prove that the HSTNet outperforms the state-of-the-art competitors both in quantitative and qualitative evaluations.

![](figs/Figure2.png)

The framework of our proposed HSTNet.

## Requirements
- Python 3.6+
- Pytorch>=1.6
- torchvision>=0.7.0
- einops
- matplotlib
- cv2
- scipy
- tqdm
- scikit


## Installation
Clone or download this code and install aforementioned requirements 
```
cd codes
```

## Train
Download the UCMerced dataset[[Baidu Drive](https://pan.baidu.com/s/1ijFUcLozP2wiHg14VBFYWw),password:terr][[Google Drive](https://drive.google.com/file/d/12pmtffUEAhbEAIn_pit8FxwcdNk4Bgjg/view)]and AID dataset[[Baidu Drive](https://pan.baidu.com/s/1Cf-J_YdcCB2avPEUZNBoCA),password:id1n][[Google Drive](https://drive.google.com/file/d/1d_Wq_U8DW-dOC3etvF4bbbWMOEqtZwF7/view)], they have been split them into train/val/test data, where the original images would be taken as the HR references and the corresponding LR images are generated by bicubic down-sample. 
```
# x4
python demo_train.py --model=HSTNET --dataset=UCMerced --scale=4 --patch_size=192 --ext=img --save=TRANSENETx4_UCMerced
# x3
python demo_train.py --model=HSTNET --dataset=UCMerced --scale=3 --patch_size=144 --ext=img --save=TRANSENETx3_UCMerced
# x2
python demo_train.py --model=HSTNET --dataset=UCMerced --scale=2 --patch_size=96 --ext=img --save=TRANSENETx2_UCMerced
```

The train/val data pathes are set in [data/__init__.py](codes/data/__init__.py) 

## Test 
The trained TransENet model on UCMerced and AID datasets can be found here [[Baidu Drive](https://pan.baidu.com/s/1lvAyTagbBf5GWUOcuEkyrQ), password:w7ct][[Google Drive](https://drive.google.com/file/d/19nH1Plh2M-Z47iXG0-Ghq-Orh33n787w/view)]. The test data path and the save path can be edited in [demo_deploy.py](codes/demo_deploy.py)

```
# x4
python demo_deploy.py --model=HSTNET --scale=4
# x3
python demo_deploy.py --model=HSTNET --scale=3
# x2
python demo_deploy.py --model=HSTNET --scale=2
```

## Evaluation 
Compute the evaluated results in term of PSNR and SSIM, where the SR/HR paths can be edited in [calculate_PSNR_SSIM.py](codes/metric_scripts/calculate_PSNR_SSIM.py)

```
cd metric_scripts 
python calculate_PSNR_SSIM.py
```
## Performance

#### Quantitative Results
![](figs/Table2.png)
![](figs/Table3.png)
![](figs/Table4.png)
Quantitative evaluation under scale factors x2, x3 and x4. The best performance is shown in **bold** and the second best performance is <u>underlined</u>.

#### More Qualitative Results (x4)

![](figs/Figure6.png)

![](figs/Figure7.png)

![](figs/Figure8.png)

![](figs/Figure9.png)

## Acknowledgements 
This code is built on [TransENet (Pytorch)](https://github.com/Shaosifan/TransENet). We thank the authors for sharing the codes.  


