<div align="center">

# NanoDet-Plus
Link to [Github Repo](https://github.com/RangiLyu/nanodet)
    
**Super fast and high accuracy lightweight anchor-free object detection model. Real-time on mobile devices.**

</div>

* ⚡Super lightweight: Model file is only 980KB(INT8) or 1.8MB(FP16).
* ⚡Super fast: 97fps(10.23ms) on mobile ARM CPU.
* 👍High accuracy: Up to **34.3 mAP<sup>val</sup>@0.5:0.95** and still realtime on CPU.
* 🤗Training friendly:  Much lower GPU memory cost than other models. Batch-size=80 is available on GTX1060 6G.
* 😎Easy to deploy: Support various backends including **ncnn, MNN and OpenVINO**. Also provide **Android demo** based on ncnn inference framework.

****

# Introduction

NanoDet is a FCOS-style one-stage anchor-free object detection model which using [Generalized Focal Loss](https://arxiv.org/pdf/2006.04388.pdf) as classification and regression loss.

In NanoDet-Plus, we propose a novel label assignment strategy with a simple **assign guidance module (AGM)** and a **dynamic soft label assigner (DSLA)** to solve the optimal label assignment problem in lightweight model training. We also introduce a light feature pyramid called Ghost-PAN to enhance multi-layer feature fusion. These improvements boost previous NanoDet's detection accuracy by **7 mAP** on COCO dataset.

****
## Benchmarks

Model          |Resolution| mAP<sup>val<br>0.5:0.95 |CPU Latency<sup><br>(i7-8700) |ARM Latency<sup><br>(4xA76) | FLOPS      |   Params  | Model Size
:-------------:|:--------:|:-------:|:--------------------:|:--------------------:|:----------:|:---------:|:-------:
NanoDet-m      | 320*320 |   20.6   | **4.98ms**           | **10.23ms**          | **0.72G**  | **0.95M** | **1.8MB(FP16)** &#124; **980KB(INT8)**
**NanoDet-Plus-m** | 320*320 | **27.0** | **5.25ms**       | **11.97ms**          | **0.9G**   | **1.17M** | **2.3MB(FP16)** &#124; **1.2MB(INT8)**
**NanoDet-Plus-m** | 416*416 | **30.4** | **8.32ms**       | **19.77ms**          | **1.52G**  | **1.17M** | **2.3MB(FP16)** &#124; **1.2MB(INT8)**
**NanoDet-Plus-m-1.5x** | 320*320 | **29.9** | **7.21ms**  | **15.90ms**          | **1.75G**  | **2.44M** | **4.7MB(FP16)** &#124; **2.3MB(INT8)**
**NanoDet-Plus-m-1.5x** | 416*416 | **34.1** | **11.50ms** | **25.49ms**          | **2.97G**   | **2.44M** | **4.7MB(FP16)** &#124; **2.3MB(INT8)**
YOLOv3-Tiny    | 416*416 |   16.6   | -                    | 37.6ms               | 5.62G      | 8.86M     |   33.7MB
YOLOv4-Tiny    | 416*416 |   21.7   | -                    | 32.81ms              | 6.96G      | 6.06M     |   23.0MB
YOLOX-Nano     | 416*416 |   25.8   | -                    | 23.08ms              | 1.08G      | 0.91M     |   1.8MB(FP16)
YOLOv5-n       | 640*640 |   28.4   | -                    | 44.39ms              | 4.5G       | 1.9M      |   3.8MB(FP16)
FBNetV5        | 320*640 |   30.4   | -                    | -                    | 1.8G       | -         |   -
MobileDet      | 320*320 |   25.6   | -                    | -                    | 0.9G       | -         |   -

***Download pre-trained models and find more models in Model Zoo or in [Release Files](https://github.com/RangiLyu/nanodet/releases)***

<details>
    <summary>Notes (click to expand)</summary>

* ARM Performance is measured on Kirin 980(4xA76+4xA55) ARM CPU based on ncnn. You can test latency on your phone with [ncnn_android_benchmark](https://github.com/nihui/ncnn-android-benchmark).

* Intel CPU Performance is measured Intel Core-i7-8700 based on OpenVINO.

* NanoDet mAP(0.5:0.95) is validated on COCO val2017 dataset with no testing time augmentation.

* YOLOv3&YOLOv4 mAP refers from [Scaled-YOLOv4: Scaling Cross Stage Partial Network](https://arxiv.org/abs/2011.08036).

</details>

****

## Model Zoo

NanoDet supports variety of backbones. Go to [config](https://github.com/RangiLyu/nanodet/tree/main/config) to see the sample training config files.

Model                 | Backbone           |Resolution|COCO mAP| FLOPS |Params | Pre-train weight |
:--------------------:|:------------------:|:--------:|:------:|:-----:|:-----:|:-----:|
NanoDet-m             | ShuffleNetV2 1.0x  | 320*320  |  20.6  | 0.72G | 0.95M | [Download](https://drive.google.com/file/d/1ZkYucuLusJrCb_i63Lid0kYyyLvEiGN3/view?usp=sharing) |
NanoDet-Plus-m-320 (***NEW***)     | ShuffleNetV2 1.0x | 320*320  |  27.0  | 0.9G  | 1.17M | [Weight](https://drive.google.com/file/d/1Dq0cTIdJDUhQxJe45z6rWncbZmOyh1Tv/view?usp=sharing) &#124; [Checkpoint](https://drive.google.com/file/d/1YvuEhahlgqxIhJu7bsL-fhaqubKcCWQc/view?usp=sharing)
NanoDet-Plus-m-416 (***NEW***)     | ShuffleNetV2 1.0x | 416*416  |  30.4  | 1.52G | 1.17M | [Weight](https://drive.google.com/file/d/1FN3WK3FLjBm7oCqiwUcD3m3MjfqxuzXe/view?usp=sharing) &#124; [Checkpoint](https://drive.google.com/file/d/1gFjyrl7O8p5APr1ZOtWEm3tQNN35zi_W/view?usp=sharing)
NanoDet-Plus-m-1.5x-320 (***NEW***)| ShuffleNetV2 1.5x | 320*320  |  29.9  | 1.75G | 2.44M | [Weight](https://drive.google.com/file/d/1Xdlgu5lxiS3w6ER7GE1mZpY663wmpcyY/view?usp=sharing) &#124; [Checkpoint](https://drive.google.com/file/d/1qXR6t3TBMXlz6GlTU3fxiLA-eueYoGrW/view?usp=sharing)
NanoDet-Plus-m-1.5x-416 (***NEW***)| ShuffleNetV2 1.5x | 416*416  |  34.1  | 2.97G | 2.44M | [Weight](https://drive.google.com/file/d/16FJJJgUt5VrSKG7RM_ImdKKzhJ-Mu45I/view?usp=sharing) &#124; [Checkpoint](https://drive.google.com/file/d/17sdAUydlEXCrHMsxlDPLj5cGb-8-mmY6/view?usp=sharing)


*Notice*: The difference between `Weight` and `Checkpoint` is the weight only provide params in inference time, but the checkpoint contains training time params.

****

## How to Train

1. **Prepare dataset**

    If your dataset annotations are pascal voc xml format, refer to [config/nanodet_custom_xml_dataset.yml](https://github.com/RangiLyu/nanodet/tree/main/config/nanodet_custom_xml_dataset.yml)

    Or convert your dataset annotations to MS COCO format[(COCO annotation format details)](https://cocodataset.org/#format-data).

2. **Prepare config file**

    Copy and modify an example yml config file in config/ folder.

    Change ***save_path*** to where you want to save model.

    Change ***num_classes*** in ***model->arch->head***.

    Change image path and annotation path in both ***data->train*** and ***data->val***.

    Set gpu ids, num workers and batch size in ***device*** to fit your device.

    Set ***total_epochs***, ***lr*** and ***lr_schedule*** according to your dataset and batchsize.

3. **Start training**

   NanoDet is now using [pytorch lightning](https://github.com/PyTorchLightning/pytorch-lightning) for training.

   For both single-GPU or multiple-GPUs, run:

   ```shell script
   python tools/train.py CONFIG_FILE_PATH
   ```

****

## Citation

```BibTeX
@misc{=nanodet,
    title={NanoDet-Plus: Super fast and high accuracy lightweight anchor-free object detection model.},
    author={RangiLyu},
    howpublished = {\url{https://github.com/RangiLyu/nanodet}},
    year={2021}
}
```
