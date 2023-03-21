# Intel OpenVINO

Our object detection model is converted from PyTorch to ONNX to OpenVINO. This is because OpenVINO accelerates the performance of machine learning models with advantages in many areas. OpenVINO integration allows inline conversion of input shape models, graph partitioning, support for INT8 models, and Docker Containers. Essentially, it provides us the model optimization necessary for our low power computer vision solution.

## Converting a PyTorch model to OpenVINO

0. If you haven't already:

    [Install OpenVINO](https://github.com/DroneVideo/docs/blob/gh-pages/openvino.md)
    
    [Install pip requirements](https://github.com/DroneVideo/docs/blob/gh-pages/setup.md) (step 3)

1. Export ONNX model

The Python script for this action can be found [here](https://github.com/DroneVideo/object-tracking-2022)

   ```shell
   python ./export_onnx.py --cfg_path ${CONFIG_PATH} --model_path ${PYTORCH_MODEL_PATH}
   ```

2. Use *onnx-simplifier* to simplify it

   ``` shell
   python -m onnxsim ${INPUT_ONNX_MODEL} ${OUTPUT_ONNX_MODEL}
   ```

3. Convert to OpenVINO

   ``` shell
   cd <INSTSLL_DIR>/openvino_2021.4.752/deployment_tools/model_optimizer
   ```

   Install requirements for convert tool

   ```shell
   sudo ./install_prerequisites/install_prerequisites_onnx.sh
   ```

   Then convert model. Notice: mean_values and scale_values should be the same with your training settings in YAML config file.
   ```shell
   python3 mo_onnx.py --input_model <ONNX_MODEL> --mean_values [103.53,116.28,123.675] --scale_values [57.375,57.12,58.395]
   ```
