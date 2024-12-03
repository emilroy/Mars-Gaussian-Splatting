# Mars Imagery with 3D Gaussian Splatting

This repository contains the work of Emil Roy and Daniel Tjandra for the MAE547 class, exploring the application of 3D Gaussian Splatting to Mars imagery.

## Setup

1. Follow the setup instructions in the [Gaussian Splatting repository](https://github.com/graphdeco-inria/gaussian-splatting/tree/54c035f7834b564019656c3e3fcc3646292f727d). This includes setting up the conda environment and installing necessary dependencies. We will be following much of the instructions found in this [Youtube Link](https://www.youtube.com/watch?v=UXtuigy_wYc) which outlines setting up Gaussian Splatting and importing your own data.

2. Download the Mars data from [this Google Drive link](https://drive.google.com/file/d/1K9FCC0Q2iMnoimP1uk_V2JxNwIgbvdXS/view?usp=sharing). Extract the data folder and place it in the cloned gaussian-splatting repository.

## Usage

After setting up the environment and adding the Mars data, follow these steps:

1. Activate the conda environment:

```
conda activate gaussian_splatting
```

2. Ensure you have a `data` folder in the gaussian-splatting repository.

3. Import images from video:

```
FFMPEG -i data/{path to desired video.mp4} -qscale:v 1 -qmin 1 -vf fps={frame extraction rate, your choice, can say 2} %04d.jpg
```

Move the created images into a newly created `input` folder.

4. Convert the data:
```
python convert.py -s data/{path to desired folder}
```
5. Train the model:
```
python train.py -s data/{path to desired folder}
```
6. View the results:
```
cd viewers/bin
SIBR_gaussianViewer_app.exe -m C:\gaussian-splatting\output\<filename>
```
Note: Turn off vsync for full framerate.

## Evaluation (Optional)

To evaluate the model:

1. Train with train/test split:
```
python train.py -s <path to COLMAP or NeRF Synthetic dataset> --eval
```
2. Generate renderings:
```
python render.py -m <path to trained model>
```
3. Compute error metrics:
```
python metrics.py -m <path to trained model>
```
## Additional Information

For more details on the 3D Gaussian Splatting method, please refer to the [original repository](https://github.com/graphdeco-inria/gaussian-splatting) and the associated paper.
