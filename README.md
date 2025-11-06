# VLA-Doc
## 1 Introduction
> Briefly describe and motivate the project:

## 2 Context
A VLA is a model that uses a pretrained backbone, which was trained on large-scale vision-language data and is subsequently trained with generating control commands. This control commands can be robot joints, end-effector poses, steering angle for a car, latent actions or mouse and keyboard commands for a virtual agent. 

Internet-scale pretraining is what theoretically gives VLAs their moat: stronger language-instruction following and better generalization across tasks and environments. 

The Vision-Language-Action field has experienced remarkable growth over the past two years.
## 3 Goals and Challenges

> one possible expoloration direction

Analysis quantization of OpenVLA and compare its containing models with other smaller VLA models.
## 4.1 Manipulation Task Approach

> openVLA model Approach

1. Simply runs the pretrained OpenVLA model without any finetuning on robotic manipulation tasks. This serves as a baseline to evaluate the model's zero-shot capabilities.
2. Using datasets in RLDS format to train VLA models for robotic manipulation tasks. RLDS (Reinforcement Learning Dataset Standard) is a standardized format for storing and sharing datasets used in reinforcement learning research.
Datasets in RLDS format:
https://robotics-transformer-x.github.io/


> evaluate models on designed tasks:

pick up object, move to location, open drawer, close drawer, push button, switch light, etc.

> evaluation criteria, describe the testing environment \
> popular VLA simulation benchmarks and what good performance looks like:
> 
**LIBERO**: >95% is expected for Spatial, Goal and Object, 90-95% is required for Long and 90, lower than 90% is only fine for static-camera-only or few-shot stuff. 

**CALVIN** is also almost saturated by current sota models like FLOWER. The benchmark has 3 main version: D (train on setup D and test on setup D), ABC (train on A,B,C and test on D) and ABCD (train on A,B,C, D and test on D). ABC is the most relevant one, as it tests generalization to unseen setups, ABCD test how well methods benefit from more diverse data and D tests fine-tuning. For CALVIN higher than 4 score for ABC is standard now and above 4.5 is sota regime. For the D version 3.75 is standard and above 4 is very good. For the ABCD version results above 4.5 are relevant.

**SIMPLER** is hard to interpret across setups; success spans 40–99% on Bridge, making cross-paper comparison noisy. For the Google Robot version current sota models achieve around 70%-80% success rate. Somehow, RLBench (the most popular 3d policy benchmark) has gained more popularity in VLA benchmarking, but all VLAs are still far away from 3D SOTA methods like 3DDA. 

Any real world results are very important and more is better, as sim-only is hard to trust especially with VLA papers that use models with 7B+ parameters and are very good in overfitting successfully on these benchmarks.


## 4.2 Driving scene understanding

> coVLA dataset and model description
CoVLA-Agent as illustrated is a VLA model designed for autonomous driving. It utilize the pretrained Llama-2 (7B) as a language model and CLIP ViT-L (224×224 pixels) as a vision encoder.

CoVLA-Agent concentrates on two tasks, which are traffic scene description generation and trajectory prediction. The model takes the ego vehicle’s speed as an input, which is transformed into an embedding vector using a Multi Layer Perceptron (MLP). The visual features extracted by CLIP ViT-L are concatenated with the speed embedding and text embedding, and then fed into the Llama-2 model. For trajectory prediction, special tokens are used as trajectory queries. The outputs of these trajectory queries are processed by an MLP layer, resulting in a sequence of 10 (x,y,z) coordinates representing the predicted trajectory of the vehicle relative to its current position, spanning a three-second time horizon.

## 5 References

@misc{reuss2025state-vla-iclr26,
          title        = {State of VLA Research at ICLR 2026},
          author       = {Reuss, Moritz},
          year         = {2025},
          month        = {October},
          howpublished = {\url{https://mbreuss.github.io/blog_post_iclr_26_vla.html}},
          note         = {Blog post},
        }

@InProceedings{covla_wacv2025,
      title     = {CoVLA: Comprehensive Vision-Language-Action Dataset for Autonomous Driving},
      author    = {Arai, Hidehisa and Miwa, Keita and Sasaki, Kento and Watanabe, Kohei and Yamaguchi, Yu and Aoki, Shunsuke and Yamamoto, Issei},
      booktitle = {Proceedings of the Winter Conference on Applications of Computer Vision (WACV)},
      month     = {February},
      year      = {2025},
      pages     = {1933-1943}
 }
