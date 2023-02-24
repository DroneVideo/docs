# Object Detection SampleSolution

This is a deployment of Nanodet's detection model, training on our own RC car and converted into an OpenVINO model. We integrate a RealSense2 camera into the demo for its ubiquitous compatibility amongstoperating systems and with Intel's OpenVINO. Realsense also has a depth camera, although it is not used in this demo.

## Build


```shell
cd {$PATH_TO_object-tracking-2022}/autodrone-openvino
mkdir build
cd build
cmake ..
make
mkdir FP32
```

## Run demo

! First, move nanodet openvino model files (.bin .xml .mapping) to the FP32 folder. Then run these commands:

### Webcam

```shell
./nanodet_demo
```

### Inference images

```shell
./nanodet_demo mode=1 IMAGE_FOLDER/*.jpg
```

### Inference video

```shell
./nanodet_demo mode=2 VIDEO_PATH
```

### Benchmark

```shell
./nanodet_demo mode=3 path=0
```

