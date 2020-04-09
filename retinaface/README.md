# RetinaFace

## Notice

- Only tested on TensorRT4
- The pytorch implementation is [biubug6/Pytorch_Retinaface](https://github.com/biubug6/Pytorch_Retinaface), I forked it into 
[wang-xinyu/Pytorch_Retinaface](https://github.com/biubug6/Pytorch_Retinaface) and add genwts.py

## Run

```
1. generate retinaface.wts from pytorch implementation https://github.com/wang-xinyu/Pytorch_Retinaface

git clone https://github.com/wang-xinyu/Pytorch_Retinaface.git
// download its weights 'Resnet50_Final.pth', put it in Pytorch_Retinaface/weights
cd Pytorch_Retinaface
python detect.py --save_model
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
sudo ./retina_r50 -s  // build and serialize model to file i.e. 'retina_r50.engine'
wget https://github.com/TencentYoutuResearch/FaceDetection-DSFD/raw/master/data/worlds-largest-selfie.jpg
sudo ./retina_r50 -d  // deserialize model file and run inference.

3. check the images generated, as follows. result.jpg
```

<p align="center">
<img src="https://user-images.githubusercontent.com/15235574/78887294-2d2d9f80-7a92-11ea-90a5-38e84a87282e.jpg">
</p>