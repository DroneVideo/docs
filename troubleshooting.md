## TroubleShooting

1. **No OpenCV**

    ```shell
    sudo apt update
    sudo apt install libopencv-dev python3-opencv
    ```

2. **No Inference Engine**

    Source OpenVINO

    ```shell
    source /opt/intel/openvino_2021/bin/setupvars.sh
    ```

3. **No Realsense2 (For camera)**

    If you do not have a RealSense camera connected to your device (through USB), this is the best error you can get.

    If you do have the camera connected, follow all the steps in the [RS2 Installation](https://github.com/DroneVideo/docs/blob/gh-pages/rs2.md)

    If you have already ran these commands and are using a virtual machine like Oracle's VirtualBox, go to the VM settings and allow your machine to access the USB port. Additionally, make sure it is expecting USB 3.0

4. **No Eigen/Eigen3**

    Solution to be posted