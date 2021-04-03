# Shoes-Manner  
Normally shoes are not allowed in Japanese houses. In such cases, there is a manner of taking off one's shoes at the entrance.
This project aims to acquire good manners. It is important to be careful in daily life to acquire manners.
https://youtu.be/hOFOsVOKmBY
![image](https://user-images.githubusercontent.com/19370970/113467245-ca8c9b00-947c-11eb-84e3-4a3fc7ab1591.png)


## Docker
```Shell
git clone --recursive https://github.com/dusty-nv/jetson-inference
cd jetson-inference
docker/run.sh
```

See this LINK for details.  
https://github.com/dusty-nv/jetson-inference/blob/master/docs/aux-docker.md  

## Pull Git  

```Shell
cd /jetson-inference/python/training/classification/data
git clone https://github.com/lucuha/Shoes-Manner.git
```

## Taking your images
```Shell
python3 still.py  --width=640 --height=480 --input-rate=1 --headless  csi://0 image/img_%04i.jpg
```

## Sorting images  
Shoes-Manner/dataset/  
-labels.txt  
-train/  
--bad/  
--good/  
-val/  
--bad/  
--good/   

labels.txt:  
```Text:labels.txt
bad
good
```

## Training your model  
```
cd /jetson-inference/python/training/classification/
cp Shoes-Manner/train2.py train2.py
python3 train2.py --model-dir=models/<YOUR-MODEL> data/Shoes-Manner/dataset
```

## Exporting onnx  
```
python3 onnx_export.py --model-dir=models/<YOUR-MODEL>
```
## Run

```
imagenet.py --model=models/shoes/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=data/Shoes-Manner/dataset/labels.txt csi://0
```
