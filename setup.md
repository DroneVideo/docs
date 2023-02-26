# Setting up our SampleSolution

Getting the object detection and tracking demos to work on your computer as fairly simply; however, installing dependencies can be time-consuming. Note that our solution is built for our onboard computer running Linux Ubuntu 20.04, so the following instructions are written for that distribution.

The first step is installing OpenVINO
[OpenVINO Installation Tutorial](https://github.com/DroneVideo/docs/blob/gh-pages/openvino.md)

RealSense libraries and packages are needed to access your RealSense2 camera
[RealSense for Linux distribution](https://github.com/DroneVideo/docs/blob/gh-pages/rs2.md)

Lastly, clone the [object-tracking-2022](https://github.com/DroneVideo/object-tracking-2022) repository and install the pip packages in the requirements.txt to create an environment that can build the SampleSolution.

```shell
pip install -r requirements.txt
```

Follow the README in that repository for instructions to build the deploy the model.