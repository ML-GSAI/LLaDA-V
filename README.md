# LLaDA-V: Large Language Diffusion Models with Visual Instruction Tuning
[![arXiv](https://img.shields.io/badge/Paper-arXiv-red.svg)](https://arxiv.org/abs/2505.16933)
[![deploy](https://img.shields.io/badge/Hugging%20Face-LLaDA_V-FFEB3B)](https://huggingface.co/GSAI-ML/LLaDA-V)


## News
- [2025.05.29] We open-sourced the model [LLaDA-V](https://huggingface.co/GSAI-ML/LLaDA-V) and the code of LLaDA-V.
- [2025.05.23] We have uploaded our paper to [arXiv](https://arxiv.org/abs/2505.16933).

  
## Introduction
 We introduce LLaDA-V, a competitive diffusion-based vision-language model, outperforming other diffusion MLLMs.


### Quick Inference Demo
The [LLaDA-V model](https://huggingface.co/GSAI-ML/LLaDA-V) is now available on Hugging Face Hub. To quickly test the model with a visual instruction demo, follow these simple steps:

1. **Clone the repository**  
   ```bash
   git clone https://github.com/ML-GSAI/LLaDA-V
   cd LLaDA-V/train
   ```
2. **Initialize the environment**  
   Run the environment setup script to install necessary dependencies:
   ```bash
   bash init_env.sh
   ```
3. **Run the demo script**  
   Execute the demo script to test LLaDA-V on an example image:
   ```bash
   python generate_demo.py
   ```

## Training
This repository includes a complete training framework for LLaDA-V, following the [LLaVA](https://github.com/haotian-liu/LLaVA) approach for visual instruction tuning. 

## Data Preparation
As an example, we outlined the data preparation process for training LLaDA-V using the LLaVA-NeXT dataset. You need to prepare the following datasets:

1. Download the LLaVA pretraining dataset from Hugging Face:
   ```
   https://huggingface.co/datasets/liuhaotian/LLaVA-Pretrain/tree/main
   ```

2. Create the directory structure `train/data/llava_pretrain` and extract `images.zip` into the `images` subfolder.

3. Ensure your `train/data/llava_pretrain` directory contains both the `images` folder and the `blip_laion_cc_sbu_558k.json` file.

4. Download the LLaVA-NeXT dataset from Hugging Face:
   ```
   https://huggingface.co/datasets/lmms-lab/LLaVA-NeXT-Data
   ```

5. Process the LLaVA-NeXT dataset by following these steps:
   - Extract all tar.gz files (from llava_next_raw_format_images_1.tar.gz to llava_next_raw_format_images_11.tar.gz) from the llava_next_raw_format folder into train/data/llava_next/images
   - Move the llava_next_raw_format_processed.json file to train/data/llava_next/

### Model Preparation

1. Download the pretrained LLaDA-8B-Instruct model from Hugging Face to the `train/model/LLaDA-8B-Instruct` directory:
   ```
   https://huggingface.co/GSAI-ML/LLaDA-8B-Instruct
   ```

2. Convert the model checkpoint to Hugging Face format by running:
   ```bash
   python train/llada_v_prepare/rename_checkpoint.py \
     --source_dir train/model/LLaDA-8B-Instruct \
     --target_dir train/model/LLaDA-8B-Instruct-HF
    
   cp train/llada_v_prepare/files/* train/model/LLaDA-8B-Instruct-HF/
   ```

3. Download the pretrained Siglip2 model from Hugging Face to the `train/model/siglip2-so400m-patch14-384` directory:
   ```
   https://huggingface.co/google/siglip2-so400m-patch14-384
   ```

### Run Scripts
```bash
Pretrain Script:
    cd train && bash scripts/llada_v_pretrain.sh

Finetune Script:
    cd train && bash scripts/llada_v_sft.sh
```

## Evaluation
We provide the evaluation code in this repository, following the [lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval) library. 

1. **Clone the repository**  
   ```bash
   git clone https://github.com/ML-GSAI/LLaDA-V
   cd LLaDA-V
   ```
2. **Initialize the environment**  
   Run the environment setup script to install necessary dependencies:
   ```bash
   bash init_env.sh
   ```
3. **Run the demo script**  
   Execute the demo script to test LLaDA-V on an example image:
   ```bash
   cd eval && bash scripts/evaluate.sh
   ```

## Contact
If you have any questions, please feel free to contact us at zebin@ruc.edu.cn.

## LLaDA Group Wechat QR Code

![LLaDA Group Wechat QR Code](./vx.jpg)

## Acknowledgments
The code is largely based on the [LLaVA-NeXT](https://github.com/LLaVA-VL/LLaVA-NeXT), [MAmmoTH-VL](https://github.com/MAmmoTH-VL/MAmmoTH-VL), [lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval) and [dLLM-cache](https://github.com/maomaocun/dLLM-cache/tree/main). We thank the authors for their great work.

## Citation

```bibtex
@article{you2025llada,
  title={LLaDA-V: Large Language Diffusion Models with Visual Instruction Tuning},
  author={You, Zebin and Nie, Shen and Zhang, Xiaolu and Hu, Jun and Zhou, Jun and Lu, Zhiwu and Wen, Ji-Rong and Li, Chongxuan},
  journal={arXiv preprint arXiv:2505.16933},
  year={2025}
}
```


