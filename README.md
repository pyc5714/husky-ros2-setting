# 0. husky ros1 docker
### 0_1. build image
```
docker pull yechanpark5714/hsk-ros1:latest
```
### 0_2. build container
```
nvidia-docker run --privileged -it \
           -e NVIDIA_DRIVER_CAPABILITIES=all \
           -e NVIDIA_VISIBLE_DEVICES=all \
           --volume=/home/husky/Desktop/husky_ROS1_docker:/home/husky_ROS1_docker \
           --volume=/tmp/.X11-unix:/tmp/.X11-unix:rw \
           --net=host \
           --ipc=host \
           --device=/dev/input/js4:/dev/input/js4 \
           --device=/dev/ttyUSB0:/dev/ttyUSB0 \
           --shm-size=2gb \
           --name=hsk_ros1 \
           --env="DISPLAY=$DISPLAY" \
           yechanpark5714/hsk-ros1:latest
```
### 0_3. install husky & launch
** 컨테이너에서 'ln -s /dev/ttyUSB0 /dev/prolific'을 통해서 심볼릭 링크 생성
```
cd /home/husky_ROS1_docker
source /opt/ros/noetic/setup.bash
source devel/setup.bash
ln -s /dev/ttyUSB0 /dev/prolific
roslaunch husky_base base.launch
```

# 1. velodyne
### Requirement
```
sudo apt install ros-foxy-diagnostic-updater
```

### 1_1. install velodyne pkg
```
git clone --branch ros2 https://github.com/ros-drivers/velodyne.git
```


### 1_2. launch
```
~/Desktop/ROS2_setting
source /opt/ros/foxy/setup.bash
source install/setup.bash
ros2 launch velodyne velodyne-all-nodes-VLP16-launch.py
```

# 2. zed2i
### Requirement
install 
```
chmod +x ZED_SDK_Ubuntu20_cuda11.8_v4.0.7.zstd.run

./ZED_SDK_Ubuntu20_cuda11.8_v4.0.7.zstd.run

  처음에만 **q** 입력하고 나머지는 다 **yes**
```
### 2_1. install zed2i pkg
```
git clone https://github.com/stereolabs/zed-ros2-wrapper.git
```
