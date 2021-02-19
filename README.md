# vibration_gan
Gan for time series vibration signals generation task, to enhance classification accuracy of fault diagnosis model by data augmentation


personal undergraduate thesis

## dataset
CWRU bearning data
[download](https://csegroups.case.edu/bearingdatacenter/pages/download-data-file)

## environment setup
- python 3.x
- tensorflow 1.15
- keras
- sklearn
- matplotlib
- numpy

## data generation 
- train gan with limited target signals:
```
$ train_gan.py --phase='train' --GAN_type='WGAN-GP' --target='B007' --imbalance_ratio=50
```
- generate target signals with pretrained gan:
```
$ train_gan.py --phase='generate' --checkpoint_dir=which-pretrained-model-in-checkpoint-dir --target='B007' --imbalance_ratio=50
```

## data evaluation
- use mmd.py to compare the difference between real data and generated data
- use tsne.py to get visualization result
- use fault_diagnosis.py to train diagnosis model with balanced dataset (generated by oversampling method - 'GAN', 'SMOTE', 'ADASYN','RANDOM')
```
$ fault_diagnosis.py --imbalance_ratio=50 --oversampling_method='GAN' --generated_data_dir='\generated_data\ORDER_minmax_ratio50'
```
- compare GAN with other oversampling method
```
$ fault_diagnosis.py --imbalance_ratio=50 --oversampling_method='ADASYN' 
```
- just train diagnosis model with balanced real dataset
```
$ fault_diagnosis.py --imbalance_ratio=1 --oversampling_method='none' 
```

## reference
[DCGAN_WGAN_WGAN-GP_LSGAN_SNGAN_RSGAN_BEGAN_ACGAN_PGGAN_TensorFlow](https://github.com/MingtaoGuo/DCGAN_WGAN_WGAN-GP_LSGAN_SNGAN_RSGAN_BEGAN_ACGAN_PGGAN_TensorFlow/blob/master/GANs.py)
