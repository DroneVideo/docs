# Installing OpenVINO Development Tools

Create a directory for OpenVINO
```shell
sudo mkdir /opt/intel/
```

Download the file at this link:
[OpenVINO 2021 for Ubuntu](https://storage.openvinotoolkit.org/repositories/openvino/packages/2021.4.2/l_openvino_toolkit_dev_ubuntu20_p_2021.4.752.tgz)

```shell
cd ~/Downloads/

tar -xf l_openvino_toolkit_dev_ubuntu20_p_2021.4.752.tgz

sudo mv l_openvino_toolkit_dev_ubuntu20_p_2021.4.752 /opt/intel/openvino_2021.4.752

cd /opt/intel/

sudo ln -s openvino_2021.4.752 openvino_2021
```

Run this command every time you set up a terminal window to use OpenVINO

```shell
source /opt/intel/openvino_2021/bin/setupvars.sh
```
*OR*
Do this once
```shell
echo source /opt/intel/openvino_2021/bin/setupvars.sh >> ~/.bashrc
```

## Installing ONNX

```shell
python3 -m venv openvino_env #(might need to sudo apt install python3.8-venv)

source openvino_env/bin/activate

python -m pip install --upgrade pip

pip install openvino-dev[ONNX]==2021.4.2
```

Test installation

```shell
mo -h
```
