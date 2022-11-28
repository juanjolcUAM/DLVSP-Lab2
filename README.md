# Introduction

This project combines YOLOv2 (reference) and SeqNMS (reference) for real time video object detection.
This guide is designed for its use on Ubuntu.

# Steps

1. Create a virtual environment with Python ver. 2.7. We will use a conda environment, for more information on how to do that you can check https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html.
    - `conda create --name EnvironmentName python=2.7`
    - `conda activate EnvironmentName`
2. Clone or download the project repository:
    - `git clone https://github.com/juanjolcUAM/DLVSP-Lab2`
3. You may need to modify the `Makefile` in order for the program to properly compile and work in your machine:
    - GPU=1 or 0 if your pc doesn't support CUDA. If you are going to execute in GPU be sure that the variables COMMON and LDFLAGS are pointing to your cuda installation folder. In this case they are pointing to `/usr/local/cuda-10.1/`.
    - CUDNN=0 or 1 if your pc does support CUDNN.
    - OPENCV=0 or 1 if your pc does support OPENCV.
4. Compile the project using `make`:
    - `cd DLVSP-Lab2`
    - `make`
5. Download the YOLOv2 and tiny YOLOv2 pretrained weights provided by pjreddie:
    - `wget https://pjreddie.com/media/files/yolo.weights`
    - `wget https://pjreddie.com/media/files/yolov2-tiny.weights`
6. Download and install the necessary libraries for running the code in the virtual environment, with the versions provided:
    - cv2: `pip install opencv-python==4.2.0.32`
    - matplotlib: `pip install matplotlib`
    - scipy: `pip install scipy`
    - pillow: `conda install -c anaconda pillow`
    - tensorflow: `conda install tensorflow=1.15`
    - tf_object_detection: `conda install -c conda-forge tf_object_detection`
7. Copy the video you want to use to the video (DLVSP-Lab2/video) folder, for example 'video.mp4'. Obtain the frames for the program by running 'video2img.py' and 'get_pkllist.py':
    - `python video2img.py -i video.mp4`
    - `python getpkllist.py`
8. Export the necessary folders for libraries
9. Return to root folder and run 'yolo_seqnms.py' to generate output images in video/output:
    - `python yolo_seqnms.py`
10. If you want to reconstruct a video from these output images, you can go to the video folder and run 'img2video.py':
    - `python img2video.py -i output`
