
1- clone the repo
```
git clone https://github.com/luiszeni/giou_faster_rcnn.git && cd giou_faster_rcnn
```

2-create the dir to extract the dataset
```
mkdir data
mkdir data/coco
cd data/coco 
```

3-download the coco data from the site
```
wget http://images.cocodataset.org/zips/train2017.zip
wget http://images.cocodataset.org/zips/val2017.zip
wget http://images.cocodataset.org/annotations/annotations_trainval2017.zip
```

4-extract coco data
```
unzip train2017.zip
unzip val2017.zip
unzip annotations_trainval2017.zip
```

5-create the images folder and move the images to it
```
mkdir images
mv train2017 images
mv val2017 images
```

It will have the following structure
  ```
  coco
  ├── annotations
  |   ├── instances_minival2014.json
  │   ├── instances_train2014.json
  │   ├── instances_train2017.json
  │   ├── instances_val2014.json
  │   ├── instances_val2017.json
  │   ├── instances_valminusminival2014.json
  │   ├── ...
  |
  └── images
      ├── train2014
      ├── train2017
      ├── val2014
      ├──val2017
      ├── ...
  ```

6-returns to root directory
```
cd ../..
```

7-get pretrained model
```
mkdir data/pretrained_model
cd data/pretrained_model
wget http://inf.ufrgs.br/~lfazeni/resnet50_caffe.pth
```

8-returns to root directory
```
cd ../..
```


9-build the docker machine
```
cd docker
docker build . -t giou
cd ..
```

10-create a container
```
docker run --gpus all -v  $(pwd):/root/giou_faster_rcnn --shm-size 12G -ti --name giou giou
```


11- Build the project inside the docker machine
```
cd lib
sh make.sh
cd ..
```


12- put the model to train
```
python3 tools/train_net_step.py --dataset coco2017 --cfg configs/baselines/e2e_faster_rcnn_R-50-FPN_giou_1x.yaml 
```

13- after training run the test script (you should update the {full_path_of_the_trained_weight} with the real path)
```
python tools/test_net.py --dataset coco2017 --cfg configs/baselines/e2e_faster_rcnn_R-50-FPN_giou_1x.yaml --load_ckpt {full_path_of_the_trained_weight}
```