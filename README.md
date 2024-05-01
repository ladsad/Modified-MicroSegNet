# Modified-MicroSegNet
Modified Official PyTorch implementation of: 

[MicroSegNet: A Deep Learning Approach for Prostate Segmentation on Micro-Ultrasound Images](https://www.sciencedirect.com/science/article/pii/S089561112400003X) (CMIG 2024)

In colaboration by:
 - Shaurya: github.com/ladsad
 - Devika Iyer: github.com/DevikaIyer23
 - Adisha Shaikh: github.com/adisha-shaikh

## Requirements
* Python==3.9.13
* torch==2.1.0
* torchvision==0.16.0
* numpy
* opencv-python
* tqdm
* tensorboard
* tensorboardX
* ml-collections
* medpy
* SimpleITK
* scipy
* `pip install -r requirements.txt`

## Dataset
- Micro-Ultrasound Prostate Segmentation Dataset
- Dataset can be accessed here: https://zenodo.org/records/10475293.

## Usage
### 1. Download Google pre-trained ViT models
* [Get models in this link](https://console.cloud.google.com/storage/vit_models/). "imagenet21k/R50+ViT-B_16.npz" is used here.
* Rename your model as: R50-ViT-B_16, ViT-B_16, ViT-L_16.....
* Save your model into folder "model/vit_checkpoint/imagenet21k/".
* If you want to use models pretrained on imagenet21k+imagenet2012, please add configs in ["TransUNet/networks/vit_seg_configs.py"](TransUNet/networks/vit_seg_configs.py)

### 2. Prepare data
* Please go to https://zenodo.org/records/10475293 to download our dataset.
* After downloading, extract the file and put it into folder "data/". The directory structure should be as follows:

```bash
.
├── data
│   ├── Micro_Ultrasound_Prostate_Segmentation_Dataset
│   │   ├── train
│   │	└── test
│   └── preprocessing.py
│
├── model
│   └── vit_checkpoint
│       └── imagenet21k
│           ├── R50+ViT-B_16.npz
│           └── *.npz
└── TransUNet

```

* Run the preprocessing script, which would generate training images in folder "train_png/", data list files in folder "lists/" and data.csv for overview.
```
python preprocessing.py
```
* Training images are preprocessed to 224*224 to feed into networks.

### 3. Train/Test
* Please go to the folder "TransUNet/" and it's ready for you to train and test the model.
```
python train_MicroUS.py
python test_MicroUS.py
```
The hard region weight here is set to 4 as default, while you can train models with different weight by specifying it in the command line as follows:
```
python train_MicroUS.py --weight 10
python test_MicroUS.py --weight 10
```

## References
* Some part of the code is adapted from [TransUNet](https://github.com/Beckschen/TransUNet) ,
which provides a very good implementation to start with.
* [ViT-pytorch](https://github.com/jeonsworld/ViT-pytorch)
* [segmentation_models.pytorch](https://github.com/qubvel/segmentation_models.pytorch)
* [MicroSegNet](https://github.com/mirthAI/MicroSegNet)

## Citations
```
@article{jiang2024microsegnet,
  title={MicroSegNet: A deep learning approach for prostate segmentation on micro-ultrasound images},
  author={Jiang, Hongxu and Imran, Muhammad and Muralidharan, Preethika and Patel, Anjali and Pensa, Jake and Liang, Muxuan and Benidir, Tarik and Grajo, Joseph R and Joseph, Jason P and Terry, Russell and others},
  journal={Computerized Medical Imaging and Graphics},
  pages={102326},
  year={2024},
  publisher={Elsevier}
}
```
