# Tracking Meets Large Multimodal Models for Driving Scenario Understanding

## Overview
This repository contains the implementation and evaluation of our method, which integrates tracking information into Large Multimodal Models (LMMs) to enhance spatiotemporal understanding in autonomous driving. By incorporating 3D object tracking, our approach significantly improves perception, planning, and prediction tasks compared to baseline models.

![Limits](https://github.com/ayesha-ishaq/TrackingMeetsLMM/blob/main/assets/example.drawio.png)

## Features
- **Enhanced VQA**: We incorporate tracking-based embeddings into VQA for autonomous driving.
- **3D Tracking Integration**: Tracks are obtained using **3DMOTFormer** and processed to provide spatiotemporal context.
- **Multimodal Fusion**: Tracks and images are combined with a multimodal language model to generate responses.
- **Self-supervised Pretraining**: We pretrain a tracking encoder to enhance context comprehension.
- **Benchmark Performance**: Our model achieves a **9.5% accuracy gain** and **7.04-point ChatGPT score improvement** over baselines on DriveLM-nuScenes, and a **3.7% final score increase** on DriveLM-CARLA.
![model](https://github.com/ayesha-ishaq/TrackingMeetsLMM/blob/main/assets/model.drawio.png)
## Data Preparation
To obtain VQA datasets, follow the instructions provided in the [DriveLM](https://github.com/OpenDriveLab/DriveLM/blob/main/challenge/README.md).

Tracks for objects and the ego-vehicle are generated using [3DMOTFormer](https://github.com/your-link-to-3dmotformer) for robust 3D multi-object tracking.

## Results
#### DriveLM-nuScenes
![Results Table 1](https://github.com/ayesha-ishaq/TrackingMeetsLMM/blob/main/assets/results_n.JPG)

#### DriveLM-CARLA
![Results Table 2](https://github.com/ayesha-ishaq/TrackingMeetsLMM/blob/main/assets/results_c.JPG)

## Setup and Fine-tuning
Refer to the setup and fine-tuning instructions available in `docs/setup_finetune.md` within this repository.

## Inference
Run the following command to perform inference on test data:
```bash
cd  llama_adapter_v2_multimodal7b/
python demo.py --llama_dir /path/to/llama_model_weights \
               --checkpoint /path/to/pre-trained/checkpoint.pth \
               --data ../test_llama.json  \
               --output ../output.json \
               --batch_size 4 \
               --num_processes 8
```

## Evaluation
First, set up the evaluation package following the instructions in [DriveLM Challenge ReadMe](https://github.com/OpenDriveLab/DriveLM/blob/main/challenge/README.md).

Then, run the evaluation script:
```bash
python evaluation/evaluation.py --root_path1 ./output.json --root_path2 ./test_eval.json
```

## Acknowledgments
We would like to acknowledge the contributions and resources from the following projects:
- [DriveLM](https://github.com/OpenDriveLab/DriveLM)
- [LLaMA Adapter](https://github.com/ZrrSkywalker/LLaMA-Adapter)
- [3DMOTFormer](https://github.com/your-link-to-3dmotformer)
- [nuScenes Dataset](https://www.nuscenes.org/)

