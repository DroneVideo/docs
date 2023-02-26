## Convert Model (already converted so no need to do this)

0. Install pip requirements
   ```shell
   pip install -r requirements.txt
   ```

1. Export ONNX model

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