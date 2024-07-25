<br>
<p align="center">
<h1 align="center"><strong>[ECCV2024] CityGaussian: Real-time High-quality Large-Scale Scene Rendering with Gaussians</strong></h1>
  <p align="center">
    Yang Liu&emsp;
    He Guan&emsp;
    Chuanchen Luo&emsp;
    Lue Fan&emsp;
    Naiyan Wang&emsp;
    Junran Peng&emsp;
    Zhaoxiang Zhang&emsp;
    <br>
    <em>Institute of Automation, Chinese Academy of Sciences; University of Chinese Academy of Sciences</em>
    <br>
  </p>
</p>

<div id="top" align="center">

[![](https://img.shields.io/badge/Paper-%F0%9F%93%96-blue)](https://arxiv.org/pdf/2404.01133)
[![](https://img.shields.io/badge/Project-%F0%9F%9A%80-blue)](https://dekuliutesla.github.io/citygs/)

</div>

The advancement of real-time 3D scene reconstruction and novel view synthesis has been significantly propelled by 3D Gaussian Splatting (3DGS). However, effectively training large-scale 3DGS and rendering it in real-time across various scales remains challenging. This paper introduces CityGaussian (CityGS), which employs a novel divide-and-conquer training approach and Level-of-Detail (LoD) strategy for efficient large-scale 3DGS training and rendering. Specifically, the global scene prior and adaptive training data selection enables efficient training and seamless fusion. Based on fused Gaussian primitives, we generate different detail levels through compression, and realize fast rendering across various scales through the proposed block-wise detail levels selection and aggregation strategy. Extensive experimental results on large-scale scenes demonstrate that our approach attains state-of-the-art rendering quality, enabling consistent real-time rendering of large-scale scenes across vastly different scales. **Welcome to visit our [Project Page](https://dekuliutesla.github.io/citygs/)**.

<!-- ![Teaser](assets/teaser.jpg) -->

<div style="text-align: center;">
    <img src="assets/Teaser.png" alt="Dialogue_Teaser" width=100% >
</div>

## 📰 News
**[2024.07.18]** Camera Ready version now can be accessed through arXiv. More insights are included.

## 🥏 Model of CityGaussian
### Training Pipeline
<p align="center">
  <img src="assets/Train.png" align="center" width="100%">
</p>

### Rendering Pipeline
<p align="center">
  <img src="assets/Render.png" align="center" width="100%">
</p>

## 🔧 Usage

Note that the configs for five large-scale scenes: MatrixCity, Rubble, Building, Residence and Sci-Art has been prepared in `config` folder.
### Training
To train a scene, config the hyperparameters of pretraining and finetuning stage with your yaml file, then replace the `COARSE_CONFIG` and `CONFIG` in `run_citygs.sh`. The `num_blocks` and `out_name` in `run_citygs.sh` should be set according to your dataset as well. Then you can train your scene by simply using:
```bash
bash run_citygs.sh
```
**Tips for adjusting the parameters on your own dataset:**
- We recommend ssim_threshold as 0.08 as a good start point
- For foreground area `aabb`, you can try our default setting first before adjusting it

### Viewer
We borrowed Web viewer from [Gaussian Lightning](https://github.com/yzslab/gaussian-splatting-lightning). Take the scene Rubble as an example. To render the scene with no LoD, you can use the following command:
```bash
python viewer.py output/rubble_c9_r4
```
To render the scene with LoD, you can use the following command:
```bash
# copy cameras.json first for direction initialization
cp output/rubble_c9_r4/cameras.json output/rubble_c9_r4_lod/
python viewer.py config/rubble_c9_r4_lod.yaml
```

## 📝 TODO List

- \[x\] First Release.
- \[ \] Release CityGaussian code.

## 📄 License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png" /></a>
<br />
This work is under the <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

## 👏 Acknowledgements

This repo benefits from [3DGS](https://github.com/graphdeco-inria/gaussian-splatting), [LightGaussian](https://github.com/VITA-Group/LightGaussian), [Gaussian Lightning](https://github.com/yzslab/gaussian-splatting-lightning). 
