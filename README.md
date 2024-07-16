# ZS6D

<img src="./assets/overview.png" width="500" alt="teaser"/>

We demonstrate the effectiveness of deep features extracted from self-supervised, pre-trained Vision Transformer (ViT) for Zero-shot 6D pose estimation. For more detailed information check out the corresponding [[paper](https://arxiv.org/pdf/2309.11986.pdf)].

## Overview of the Pipeline:

![pipeline](./assets/ZS6D_pipeline.png)

Note that this repo only deals with 6D pose estimation, you need segmentation masks as input. These can be obtained with supervised trained methods or zero-shot methods. For zero-shot we refer to [cnos](https://github.com/nv-nguyen/cnos).

## Installation:
To setup the environment to run the code locally follow these steps:

```
conda env create -f environment.yml
conda activate zs6d
```

Otherwise, run the following commands:

```
conda create --name zs6d python=3.9
conda activate zs6d
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 -c pytorch -c nvidia
pip install tqdm==4.65.0
pip install timm==0.9.16
pip install matplotlib==3.8.3
pip install scikit-learn==1.4.1.post1
pip install git+https://github.com/lucasb-eyer/pydensecrf.git@dd070546eda51e21ab772ee6f14807c7f5b1548b
pip install transforms3d==0.4.1
pip install pillow==9.4.0
pip install plyfile==1.0.3
pip install trimesh==4.1.4
pip install imageio==2.34.0
pip install pypng==0.20220715.0
pip install vispy==0.12.2
pip install pyopengl==3.1.1a1
pip install pyglet==2.0.10
pip install numba==0.59.0
pip install jupyter==1.0.0

pip install opencv-python
```


### Docker setup:

### ROS integration:

## Template rendering:
To generate templates from a object model to perform inference, we refer to the [ZS6D_template_rendering](https://github.com/haberger/ZS6D_template_rendering) repository.

## Template preparation:

1. set up a config file for template preparation

```zs6d_configs/template_gt_preparation_configs/your_template_config.json```

2. run the preparation script with your config_file to generate your_template_gt_file.json and prepare the template descriptors and template uv maps

```python3 prepare_templates_and_gt.py --config_file zs6d_configs/template_gt_preparation_configs/your_template_config.json```


## Inference:
After setting up your_template_config.json you can instantiate your ZS6D module and perform inference. An example is provided in:

```test_zs6d.ipynb```


## Evaluation on BOP Datasets:

1. set up a config file for BOP evaluation

```zs6d_configs/bop_eval_configs/your_eval_config.json```

2. Create a ground truth file for testing, the files for BOP'19-23 test images are provided for lmo, tless and ycbv. For example for lmo:

```gts/test_gts/lmo_bop_test_gt_sam.json```

Additionally, you have to download the corresponding [BOP test images](https://bop.felk.cvut.cz/datasets/#LM-O). If you want to test another dataset as the provided, you have to generate a ground truth file with the following structure:

```json
{
  "object_id": [
    {
      "scene_id": "00001", 
      "img_name": "relative_path_to_image/image_name.png", 
      "obj_id": "..", 
      "bbox_obj": [], 
      "cam_t_m2c": [], 
      "cam_R_m2c": [], 
      "cam_K":[],
      "mask_sam": [] // mask in RLE encoding
    }
    ,...
  ]
}
```

3. run the evaluation script with your_eval_config.json

```python3 prepare_templates_and_gt.py --config_file zs6d_configs/template_gt_preparation_configs/your_eval_config.json```


## Acknowledgements
This project is built upon [dino-vit-features](https://github.com/ShirAmir/dino-vit-features), which performed a very comprehensive study about features of self-supervised pretrained Vision Transformers and their applications, including local correspondence matching. Here is a link to their [paper](https://arxiv.org/abs/2112.05814). We thank the authors for their great work and repo.

## Citation
If you found this repository useful please consider starring ⭐ and citing :

```
@article{ausserlechner2023zs6d,
  title={ZS6D: Zero-shot 6D Object Pose Estimation using Vision Transformers},
  author={Ausserlechner, Philipp and Haberger, David and Thalhammer, Stefan and Weibel, Jean-Baptiste and Vincze, Markus},
  journal={arXiv preprint arXiv:2309.11986},
  year={2023}
}
```
