## Semantic Video Segmentation by Gated Recurrent Flow Propagation
This repo contains the code for the CVPR 2018 paper "Semantic Video Segmentation by Gated Recurrent Flow Propagation" by David Nilsson and Cristian Sminchisescu. [[pdf]](http://openaccess.thecvf.com/content_cvpr_2018/papers/Nilsson_Semantic_Video_Segmentation_CVPR_2018_paper.pdf)

### Setup

Check config.py. Download all data from the cityscapes dataset and change the paths in config.py. Check that you can run python config.py without any errors.

Run misc/compile.sh to compile the bilinear warping operator. Change the include directory on line 9 if you get errors related to libcudart.

Download all pretrained models from [here](https://drive.google.com/open?id=1eGy7JcX1ptzxwQ6thEd2R_ix4VehLRQL) and unpack them under ./checkpoints/. For instance, the file ./checkpoints/flownet1.index should exist.

### Evaluate a Pre-Trained Model

Evaluate the GRFP(LRR-4x, FlowNet2) setup on the validation set by running:
```
python evaluate.py --static lrr --flow flownet2
```

Evalutate GRFP(Dilation10, FlowNet2) for various number of frames, as in Table 3 and 4 in the paper:
```
python evaluate.py --static dilation --flow flownet2 --frames 1
python evaluate.py --static dilation --flow flownet2 --frames 5
```

The values in table 9 can be reproduced by running the following:
```
python evaluate.py --static lrr --flow flownet2
python evaluate.py --static lrr --flow flownet1
python evaluate.py --static lrr --flow farneback
```

### Training

Train and evaluate a model with the following commands:
```
python train.py --static lrr --flow flownet2
python evaluate.py --static lrr --flow flownet2 --ckpt lrr_flownet2_it10000
```
This should match the performance of the pre-trained LRR model above. See the ./checkpoints directory where parameters are saved during the training procedure. Only LRR is supported at the moment.

### Citation
If you use the code in your own research, please cite
```
@InProceedings{Nilsson_2018_CVPR,
author = {Nilsson, David and Sminchisescu, Cristian},
title = {Semantic Video Segmentation by Gated Recurrent Flow Propagation},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2018}
}
```

Depending on the setup you use, consider also citing [PSP](https://github.com/hszhao/PSPNet), [LRR](https://github.com/golnazghiasi/LRR), [Dilation](https://github.com/fyu/dilation), [FlowNet1](https://lmb.informatik.uni-freiburg.de/Publications/2015/DFIB15/), [FlowNet2](https://github.com/lmb-freiburg/flownet2) or [Farnebäck](https://link.springer.com/chapter/10.1007/3-540-45103-X_50).