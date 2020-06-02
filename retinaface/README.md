# RetinaFace

## Notice

- Tested on TX2/TensorRT4 and GTX1080/TensorRT7
- The pytorch implementation is [biubug6/Pytorch_Retinaface](https://github.com/biubug6/Pytorch_Retinaface), I forked it into 
[wang-xinyu/Pytorch_Retinaface](https://github.com/biubug6/Pytorch_Retinaface) and add genwts.py

## Run Resnet50

```
1. generate retinaface.wts from pytorch implementation https://github.com/wang-xinyu/Pytorch_Retinaface

git clone https://github.com/wang-xinyu/Pytorch_Retinaface.git
// download its weights 'Resnet50_Final.pth', put it in Pytorch_Retinaface/weights
// https://pan.baidu.com/s/12h97Fy1RYuqMMIV-RpzdPg   Password: fstq
cd Pytorch_Retinaface
python detect.py --save_model retinaface.pth
python genwts.py
// a file 'retinaface.wts' will be generated.

2. put retinaface.wts into tensorrtx/retinaface, build and run

git clone https://github.com/wang-xinyu/tensorrtx.git
cd tensorrtx/retinaface
// put retinaface.wts here
mkdir build
cd build
cmake ..
make
sudo ./retina_50 -s  // build and serialize model to file i.e. 'retina_r50.engine'
wget https://github.com/TencentYoutuResearch/FaceDetection-DSFD/raw/master/data/worlds-largest-selfie.jpg
sudo ./retina_50 -d  // deserialize model file and run inference.

3. check the images generated, as follows. result.jpg
```

<p align="center">
<img src="https://user-images.githubusercontent.com/15235574/78901890-9077fb80-7aab-11ea-94f1-237f51fcc347.jpg">
</p>

## Run mobilenet0.25

```
1. generate mobilenet0.25.wts from pytorch implementation https://github.com/wang-xinyu/Pytorch_Retinaface

git clone https://github.com/wang-xinyu/Pytorch_Retinaface.git
// download its weights 'mobilenet0.25_Final.pth', put it in Pytorch_Retinaface/weights
// https://pan.baidu.com/s/12h97Fy1RYuqMMIV-RpzdPg   Password: fstq
cd Pytorch_Retinaface
python detect.py --network mobile0.25 --trained_model ./weights/mobilenet0.25_Final.pth --save_model mobilenet0.25.pth
python genwts_mobile0.25.py
// a file 'retinaface.wts' will be generated.

2. put mobilenet0.25.wts into tensorrtx/retinaface, build and run

git clone https://github.com/wang-xinyu/tensorrtx.git
cd tensorrtx/retinaface_mobile0.25
// put mobilenet0.25.wts here
mkdir build
cd build
cmake ..
make
sudo ./mobile_0.25 -s  // build and serialize model to file i.e. 'retina_r50.engine'
wget https://github.com/TencentYoutuResearch/FaceDetection-DSFD/raw/master/data/worlds-largest-selfie.jpg
sudo ./mobile_0.25 -d  // deserialize model file and run inference.

3. check the images generated, as follows. result.jpg
```
