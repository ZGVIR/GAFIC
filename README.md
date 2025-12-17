# Global-Attention-fused-Image-Cropping

This is the official repository for the following paper:

> **Global Attention-fused Image Cropping with Attention-guided and Global-aligned Crop Evaluator** [[arxiv]](https://arxiv.org/pdf/2207.10269.pdf)
>
> Haotian Yang, Zhile Yang, Mubai Li, Kin-Man Lam, Senior Member, IEEE, Xin Sun, Senior Member, IEEE<br>
> Accepted by **ECCV2022**.

Our study focuses on image cropping which aims to  improve the aesthetic quality of an image by capturing important content. To this end, we propose Global Attention-Fused Image Cropping (GAFIC), a novel framework, to address the issues of coarse attention distribution and poor perception of regions near cropping boundaries during feature representation. As illustrated in the figure below, the proposed framework is composed of two key components: Attention-Guided Feature Fusion (AGFF) and Global-Aligned Crop Evaluator (GACE). AGFF generates one global feature to represent
the importance of each local region. GACE aligns and fuses the features of the cropping regions with the global feature to make it sensitive to the boundary of the cropping box.

<div align="center">
  <img src='https://github.com/ZGVIR/GAFIC/blob/main/figure/pipeline.png' align="center" width=800>
</div>

## Results

In the below figure, we present the existing state-of-the-art methods side by side with our method, which demonstrates that our method outperforms other existing methods in terms of expression of the importance of different local regions and perception ability of the boundary areas of the cropping boxes. For images with clear objects in columns (A), (D), and (E), our results on different types of images are close to the true values. For example, foot movement is truncated by VEN [36] when a person is in the center of the image (A), while our method retains the details of the foot movement while highlighting the object.

<div align="center">
  <img src='https://github.com/ZGVIR/GAFIC/blob/main/figure/qaulitative_comparison.png' align="center" width=800>
</div>


## Usage

Here we not only release the code of our method, but also provide the selected human-centric samples in these frequently used image cropping datasets, 
as well as their human bounding boxes under the folder 
[``human_bboxes``](https://github.com/bcmi/Human-Centric-Image-Cropping/tree/main/human_bboxes).

1. Download the source code and related image cropping datasets including CPC, GAICD, FCDB, and FLMS datasets. 
The homepages of these datasets have been summarized in our another repository 
[``Awesome-Aesthetic-Evaluation-and-Cropping``](https://github.com/bcmi/Awesome-Aesthetic-Evaluation-and-Cropping).

2. Change the pathes to above datasets and annotation files in ``config_GAICD.py`` and ``config_CPC.py``.

3. Run the following bash commands  
``docker pull lingyun92888/crop:250816-2``  
``mount /dev/nvme1n1p1 ebs``  
``docker run -itd --gpus all -v path-to-your-directory:/root/Human-Centric-Image-Cropping lingyun92888/crop:250816-2``  
``docker exec -it container_id bash``  
``cd path-to-your-directory``  


4. Run ``generate_pseudo_heatmap.py`` to generate pseudo heatmaps for GAICD or CPC dataset. 

5. Install the RoI&RoDAlign libraries following the instruction of [GAICD](https://github.com/HuiZeng/Grid-Anchor-based-Image-Cropping-Pytorch).

6. Run ``train_on_GAICD.py`` (*resp.*, ``train_on_CPC.py``) to train a new model on GAICD dataset (*resp.*, CPC dataset).

### Requirements
Please see [``requirement.txt``](./requirements.txt).

## Other Resources

+ [Awesome-Aesthetic-Evaluation-and-Cropping](https://github.com/bcmi/Awesome-Aesthetic-Evaluation-and-Cropping)

## Acknowledgement<a name="codesource"></a> 

This implementation borrows from [GAICD](https://github.com/HuiZeng/Grid-Anchor-based-Image-Cropping-Pytorch).
