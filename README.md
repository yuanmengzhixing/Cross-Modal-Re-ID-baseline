# Cross-Modal-Re-ID-baseline
Pytorch Code for Cross-Modality Person Re-Identification (Visible Thermal Re-ID) on RegDB dataset [1] and SYSU-MM01 dataset [2]. 

We adopt the two-stream network structure introduced in [3]. ResNet50 is adopted as the backbone. The softmax loss is adopted as the baseline. 

|Datasets    | Pretrained| Rank@1  | mAP | Model|
| --------   | -----    | -----  |  -----  | ----- |
|#RegDB      | ImageNet | ~ 22.4% | ~ 22.8% | ----- |
|#SYSU-MM01  | ImageNet | ~ 24.5%  | ~ 27.2% | [GoogleDrive](https://drive.google.com/open?id=1eLGMK3Hg413iW3IBKrB43kMWLvikbZGH)|

*Both of these two datasets may have some fluctuation due to random spliting. The results might be better by finetuning the hyper-parameters. 

### 1. Prepare the datasets.

- (1) RegDB Dataset [1]: The RegDB dataset can be downloaded from this [website](http://dm.dongguk.edu/link.html) by submitting a copyright form.

    - (Named: "Dongguk Body-based Person Recognition Database (DBPerson-Recog-DB1)" on their website). 

    - A private download link can be requested via sending me an email (mangye16@gmail.com). 
  
- (2) SYSU-MM01 Dataset [2]: The SYSU-MM01 dataset can be downloaded from this [website](http://isee.sysu.edu.cn/project/RGBIRReID.htm).

   - run `python pre_process_sysu.py` to pepare the dataset, the training data will be stored in ".npy" format.

### 2. Training.
  Train a model by
  ```bash
python train.py --dataset sysu --lr 0.01 --drop 0.0 --trial 1 --gpu 1
```

  - `--dataset`: which dataset "sysu" or "regdb".

  - `--lr`: initial learning rate.
  
  -  `--drop`: dropout ratio.
  
  -  `--trial`: training trial (only for RegDB dataset).

  -  `--gpu`: which gpu to run.

More parameters can be found in the script. You may need mannully define the data path first.

The training log will be saved in `log/" dataset_name"+ log`. Model will be saved in `save_model/`

### 3. Testing.

Test a model on SYSU-MM01 dataset by 
  ```bash
python test.py --mode all --resume 'model_path' --gpu 1
```

  - `--mode`: "all" or "indoor" all search or indoor search.
  
  - `--resume`: the saved model path.
  
  - `--gpu`:  which gpu to run.

###  4. Tips.
 - Dropout ratio is very important for the small RegDB dataset (`--drop 0.5`).
 
 - Softmax loss is not good on RegDB dataset, triplet loss performs much better on this dataset.
 
###  5. References.
[1] D. T. Nguyen, H. G. Hong, K. W. Kim, and K. R. Park. Person recognition system based on a combination of body images from visible
light and thermal cameras. Sensors, 17(3):605, 2017.

[2] A. Wu, W.-s. Zheng, H.-X. Yu, S. Gong, and J. Lai. Rgb-infrared crossmodality person re-identification. In IEEE International Conference on Computer Vision (ICCV), pages 5380–5389, 2017.

[3]  M. Ye, Z. Wang, X. Lan, and P. C. Yuen. Visible thermal person reidentification via dual-constrained top-ranking. In International Joint Conference on Artificial Intelligence (IJCAI), pages 1092–1099, 2018.

Contact: mangye16@gmail.com
