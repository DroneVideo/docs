# ByteTrack

#### ByteTrack is a simple, fast and strong multi-object tracker.

> [**ByteTrack: Multi-Object Tracking by Associating Every Detection Box**](https://github.com/ifzhang/ByteTrack)

## Introduction
Multi-object tracking (MOT) aims at estimating bounding boxes and identities of objects in videos. Most methods obtain identities by associating detection boxes whose scores are higher than a threshold. The objects with low detection scores, e.g. occluded objects, are simply thrown away, which brings non-negligible true object missing and fragmented trajectories. To solve this problem, we present a simple, effective and generic association method, tracking by associating every detection box instead of only the high score ones. For the low score detection boxes, we utilize their similarities with tracklets to recover true objects and filter out the background detections. When applied to 9 different state-of-the-art trackers, our method achieves consistent improvement on IDF1 scores ranging from 1 to 10 points. To put forwards the state-of-the-art performance of MOT, we design a simple and strong tracker, named ByteTrack. For the first time, we achieve 80.3 MOTA, 77.3 IDF1 and 63.1 HOTA on the test set of MOT17 with 30 FPS running speed on a single V100 GPU.

## Model zoo

* **Standard models**

| Model    |  MOTA | IDF1 | IDs | FPS |
|------------|-------|------|------|------|
|bytetrack_x_mot17 [[google]](https://drive.google.com/file/d/1P4mY0Yyd3PPTybgZkjMYhFri88nTmJX5/view?usp=sharing), [[baidu(code:ic0i)]](https://pan.baidu.com/s/1OJKrcQa_JP9zofC6ZtGBpw) | 90.0 | 83.3 | 422 | 29.6 |
|bytetrack_l_mot17 [[google]](https://drive.google.com/file/d/1XwfUuCBF4IgWBWK2H7oOhQgEj9Mrb3rz/view?usp=sharing), [[baidu(code:1cml)]](https://pan.baidu.com/s/1242adimKM6TYdeLU2qnuRA) | 88.7 | 80.7 | 460 | 43.7 |
|bytetrack_m_mot17 [[google]](https://drive.google.com/file/d/11Zb0NN_Uu7JwUd9e6Nk8o2_EUfxWqsun/view?usp=sharing), [[baidu(code:u3m4)]](https://pan.baidu.com/s/1fKemO1uZfvNSLzJfURO4TQ) | 87.0 | 80.1 | 477 | 54.1 |
|bytetrack_s_mot17 [[google]](https://drive.google.com/file/d/1uSmhXzyV1Zvb4TJJCzpsZOIcw7CCJLxj/view?usp=sharing), [[baidu(code:qflm)]](https://pan.baidu.com/s/1PiP1kQfgxAIrnGUbFP6Wfg) | 79.2 | 74.3 | 533 | 64.5 |

* **Light models**

| Model    |  MOTA | IDF1 | IDs | Params(M) | FLOPs(G) |
|------------|-------|------|------|------|-------|
|bytetrack_nano_mot17 [[google]](https://drive.google.com/file/d/1AoN2AxzVwOLM0gJ15bcwqZUpFjlDV1dX/view?usp=sharing), [[baidu(code:1ub8)]](https://pan.baidu.com/s/1dMxqBPP7lFNRZ3kFgDmWdw) | 69.0 | 66.3 | 531 | 0.90 | 3.99 |
|bytetrack_tiny_mot17 [[google]](https://drive.google.com/file/d/1LFAl14sql2Q5Y9aNFsX_OqsnIzUD_1ju/view?usp=sharing), [[baidu(code:cr8i)]](https://pan.baidu.com/s/1jgIqisPSDw98HJh8hqhM5w) | 77.1 | 71.5 | 519 | 5.03 | 24.45 |

## Training

First, you need to prepare your dataset in COCO format. You can refer to [MOT-to-COCO](https://github.com/ifzhang/ByteTrack/blob/main/tools/convert_mot17_to_coco.py) or [CrowdHuman-to-COCO](https://github.com/ifzhang/ByteTrack/blob/main/tools/convert_crowdhuman_to_coco.py). Then, you need to create a Exp file for your dataset. You can refer to the [CrowdHuman](https://github.com/ifzhang/ByteTrack/blob/main/exps/example/mot/yolox_x_ch.py) training Exp file. Don't forget to modify get_data_loader() and get_eval_loader in your Exp file. Finally, you can train bytetrack on your dataset by running:

```shell
cd <ByteTrack_HOME>
python3 tools/train.py -f exps/example/mot/your_exp_file.py -d 8 -b 48 --fp16 -o -c pretrained/yolox_x.pth
```

## Applying BYTE to other trackers

See [tutorials](https://github.com/ifzhang/ByteTrack/tree/main/tutorials).

## Combining BYTE with other detectors

Suppose you have already got the detection results 'dets' (x1, y1, x2, y2, score) from other detectors, you can simply pass the detection results to BYTETracker (you need to first modify some post-processing code according to the format of your detection results in [byte_tracker.py](https://github.com/ifzhang/ByteTrack/blob/main/yolox/tracker/byte_tracker.py)):

```
from yolox.tracker.byte_tracker import BYTETracker
tracker = BYTETracker(args)
for image in images:
   dets = detector(image)
   online_targets = tracker.update(dets, info_imgs, img_size)
```

## Citation

```BibTeX
@article{zhang2022bytetrack,
  title={ByteTrack: Multi-Object Tracking by Associating Every Detection Box},
  author={Zhang, Yifu and Sun, Peize and Jiang, Yi and Yu, Dongdong and Weng, Fucheng and Yuan, Zehuan and Luo, Ping and Liu, Wenyu and Wang, Xinggang},
  booktitle={Proceedings of the European Conference on Computer Vision (ECCV)},
  year={2022}
}
```
