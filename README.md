# RetinaNet-mxnet
Adapted from [SSD](https://github.com/zhreshold/mxnet-ssd) implemented by zhreshold, the results still need to be tuned. Currently we use the PASCAL VOC mAP metric which measures under IoU threshold 0.5, not the COCO AP metric.
### Differences from SSD
* We build FPN (P3 to P7) to replace the "multi_layer_feature" function;
* We build cls_subnet and bbox_subnet in the "multibox_layer" function, and the bias is initialized according to the [Focal Loss paper](https://arxiv.org/abs/1708.02002) (only for FL strategy);
* We use the anchor setting in the focal loss paper which is tested on COCO, but the best setting for PASCAL VOC still needs to be tuned;
* We adopt the [focal loss operator](https://github.com/eldercrow/focal_loss_mxnet_ssd) by eldercrow;
* We support converting COCO2017 data to rec format for training and validation.

### Usage
* Download COCO2017 data and annotations;
* Run tools/prepare_coco.sh to pack into rec format, after configuring your own paths;
* Run train-COCO2017.sh after configuring your own paths and hyperparamters.

For PASCAL VOC and more details, one can generally refer to [SSD](https://github.com/zhreshold/mxnet-ssd) implemented by zhreshold.

### Environment
Tested on Ubuntu 16.04, python3.5, mxnet 1.1.0

Numpy, cv2 and matplotlib are required.

### mAP result
|    Model    |    Training data    |    Val data    |    Strategy    |    mAP    |    Note    |
|:----------------:|:---------------:|:------------:|:---------------:|:------:|:---------------|
| ResNet-50 512x512 | VOC07+12 trainval | VOC07 test | OHEM | 78.8 | sgd, lr0.01 |
| ResNet-50 512x512 | VOC07+12 trainval | VOC07 test | FL |  | adam, lr0.0005 |
| ResNet-50 512x512 | COCO2017 train | COCO2017 val | OHEM |  | sgd, lr0.01 |
| ResNet-50 512x512 | COCO2017 train | COCO2017 val | FL |  | sgd, lr0.01 |
