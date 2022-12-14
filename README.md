# Seq_nms_YOLO

#### Members: Juan José López Castilla and Shuo Gou
#### Original members: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines [**YOLOv2**](https://arxiv.org/abs/1506.02640) and [**Seq-NMS**](https://arxiv.org/abs/1602.08465) for **real time video object detection**.
This guide is designed for its use on Ubuntu.

## Steps

1. Create a virtual environment with Python ver. 2.7. We will use a conda environment, for more information on how to do that you can check https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html.
```
    conda create --name EnvironmentName python=2.7
    conda activate EnvironmentName
```

2. Clone or download the project repository:
```
    git clone https://github.com/juanjolcUAM/DLVSP-Lab2
```

3. You may need to modify the `Makefile` in order for the program to properly compile and work in your machine:
    - GPU=1, or 0 if your pc doesn't support CUDA. If you are going to execute in GPU be sure that the variables COMMON and LDFLAGS are pointing to your CUDA installation folder. In this case they are pointing to `/usr/local/cuda/`.
    - CUDNN=1, or 0 if your pc does not support CUDNN.
    - OPENCV=1, or 0 if your pc does not support OPENCV.

4. Compile the project using `make`:
```
    cd DLVSP-Lab2
    make
```

5. Download the YOLOv2 and tiny YOLOv2 pretrained weights provided by Joseph Chet Redmon ([pjreddie](https://pjreddie.com)) in his website:
```
    wget https://pjreddie.com/media/files/yolo.weights
    wget https://pjreddie.com/media/files/yolov2-tiny.weights
```

6. Download and install the necessary libraries for running the code in the virtual environment, with the versions provided:
    - cv2: `pip install opencv-python==4.2.0.32`
    - matplotlib: `pip install matplotlib`
    - scipy: `pip install scipy`
    - pillow: `conda install -c anaconda pillow`
    - tensorflow: `conda install tensorflow=1.15`
    - tf_object_detection: `conda install -c conda-forge tf_object_detection`

7. Copy your libdarknet object and link files (`libdarknet.so` and `libdarknet.a`) to the library folder of your virtual environment. Using conda, you can know where the base environment folder is by executing `which python` while in the environment, and accessing `../..` from there. Then the folder `lib` would be the library folder.

8. Copy the video you want to use to the video folder (`DLVSP-Lab2/video`), for example 'video.mp4'. Obtain the frames for the program by running `video2img.py` and `get_pkllist.py`:
```
    python video2img.py -i video.mp4
    python get_pkllist.py
```
9. Return to root folder and run `yolo_seqnms.py` to generate output images in `DLVSP-Lab2/video/output`:
```
    python yolo_seqnms.py
```
10. If you want to reconstruct a video from these output images, you can go to the video folder and run `img2video.py`:
```
    python img2video.py -i output
```

## References

This project uses code from the repositories [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).

This repository is a fork of [seq_nms_yolo](https://github.com/melodiepupu/seq_nms_yolo), with the purpose of making these instructions clearer and easier to follow.