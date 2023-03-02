# Setting up our SampleSolution

Getting the object detection and tracking demos to work on your computer as fairly simply; however, installing dependencies can be time-consuming. Note that our solution is built for our onboard computer running Linux Ubuntu 20.04, so the following instructions are written for that distribution.

1.  The first step is installing OpenVINO
    [OpenVINO Installation Tutorial](https://github.com/DroneVideo/docs/blob/gh-pages/openvino.md)

2.  RealSense libraries and packages are needed to access your RealSense2 camera
    [RealSense for Linux distribution](https://github.com/DroneVideo/docs/blob/gh-pages/rs2.md)

3.  Lastly, clone the [object-tracking-2022](https://github.com/DroneVideo/object-tracking-2022) 
    repository and install the pip packages in the requirements.txt to create an environment that can build the SampleSolution.

    ```shell
    pip install -r requirements.txt
    ```

4.  Follow the README in that repository for instructions to build the deploy the model.

## Demo with BYTETrack (not benchmarked)

In addition to our object detection model with NanoDet, we produced an object tracking method combining NanoDet and BYTETrack. Given an initial frame containing the rover, NanoDet detects the rover and from there BYTETrack uses its region based tracking to compare frames and track the rover. We use ROS to publish the coordinates of rover and to access the RealSense camera.

1. Install ROS and setup a catkin workspace
    [ROS Noetic Installation](https://github.com/DroneVideo/docs/blob/gh-pages/ros.md)

    ```shell
    mkdir ~/catkin_ws/src
    cd ~/catkin_ws/
    catkin_make
    ```

    You now should have a build, devel, and src folder in catkin. Source devel.

    ```shell
    source devel/setup.bash
    ```

2. Clone the [bytetrack-demo-2023](https://github.com/DroneVideo/bytetrack-demo-2023) repository into ~/catkin_ws/src/

3. Follow the instructions from the README found in that repo