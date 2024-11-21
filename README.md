# Installation
I got useful information from this website before creating this project by updating something to avoid errors. Thanks to the authors! ([url](https://github.com/Mauhing/ORB_SLAM3/blob/master/README.md), [video](https://www.youtube.com/watch?v=DxqzwBQVCNw)) and [url](https://github.com/thien94/ORB_SLAM3/tree/67c18ebc3ef884409a7cab1892203ece7066e82a)



#  Prerequisites


## Ubuntu 20.04
## Pangolin
## OpenCV
## ROS


# 1. Installation of ORB-SLAM 3 on a freshly installed (CPU) Ubuntu 20.04
Install all library dependencies.
``` shell

sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
sudo apt update

sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev libjasper-dev

sudo apt-get install libglew-dev libboost-all-dev libssl-dev

sudo apt install libeigen3-dev

```
---

### Install Pangolin
Now, we install the Pangolin. 
```shell
cd ~/Dev
git clone https://github.com/stevenlovegrove/Pangolin.git
cd Pangolin 
mkdir build 
cd build 
cmake .. -D CMAKE_BUILD_TYPE=Release 
make -j 3 
sudo make install
```
> If you want to install to conda environment, add `CMAKE_INSTALL_PREFIX=$CONDA_PREFIX` instead.
---



### Install OpenCV 4.4.0
The ORB-SLAM 3 was test by  
```shell
cd ~
mkdir Dev && cd Dev
git clone https://github.com/opencv/opencv.git
cd opencv
git checkout 4.4.0
mkdir build
cd build
cmake ..
make -j4
sudo make install
```
Now check the openCV version by opening a new terminal:

```shell
python3
import cv2
cv2.__version__
```
Should be see:

```shell
'4.4.0'
```




### ORB-SLAM 3
Now, we install ORB-SLAM3. I used the commit version ef9784101fbd28506b52f233315541ef8ba7af57 tag: v0.3-beta

```shell
cd ~/Dev
git clone https://github.com/thien94/ORB_SLAM3.git ORB_SLAM3
# Build
cd ORB_SLAM3
chmod +x build.sh
./build.sh
```


# 2. Download test datasets

```shell
cd ~
mkdir -p Datasets/EuRoc
cd Datasets/EuRoc/
wget -c http://robotics.ethz.ch/~asl-datasets/ijrr_euroc_mav_dataset/machine_hall/MH_01_easy/MH_01_easy.zip
mkdir MH01
unzip MH_01_easy.zip -d MH01/

```
Similar to other datasets in EuRoc, see here  ([url](https://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets), [url](https://github.com/Mauhing/ORB_SLAM3/blob/master/README.md), and [url](https://github.com/thien94/ORB_SLAM3/tree/67c18ebc3ef884409a7cab1892203ece7066e82a))



# 3. Run  

**Simulation**
```shell
cd ~/Dev/ORB_SLAM3
# Mono + Inertial
./Examples/Monocular-Inertial/mono_inertial_euroc ./Vocabulary/ORBvoc.txt ./Examples/Monocular-Inertial/EuRoC.yaml ~/Datasets/EuRoC/MH01 ./Examples/Monocular-Inertial/EuRoC_TimeStamps/MH01.txt dataset-MH01_monoimu

```

**Live with RealSense_D435i**
```shell
cd ~/Dev/ORB_SLAM3

 ./Examples/Monocular-Inertial/mono_inertial_realsense_D435i Vocabulary/ORBvoc.txt ./Examples/Monocular-Inertial/RealSense_D435i.yaml
``

