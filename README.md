# EEG-to-Text Decoding

This repository contains code for decoding text from EEG signals using the ZuCo dataset.

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/DhRUVwol/EEG-To-Text-Decoding.git
cd EEG-To-Text-Decoding
```

### 2. Install Dependencies
```bash
pip install torch transformers nltk rouge bert-score tensorboard tqdm numpy scipy h5py
```

### 3. Download ZuCo Dataset
The dataset is not included in this repository due to size constraints. You need to:

1. Download the ZuCo dataset from the official source
2. Place the dataset files in the following structure:
```
dataset/
├── ZuCo/
│   ├── task1-SR/
│   │   └── Matlab_files/
│   ├── task2-NR/
│   │   └── Matlab_files/
│   ├── task2-NR-2.0/
│   │   └── Matlab_files/
│   └── task3-TSR/
│       └── Matlab_files/
```

### 4. Prepare Dataset
Run the dataset preparation script:
```bash
bash scripts/prepare_dataset_raw.sh
```

This will:
- Convert .mat files to .pickle format
- Generate sentiment labels
- Create necessary directory structure

### 5. Train the Model
```bash
bash scripts/train_decoding_raw.sh
```

## Project Structure
- `train_decoding_raw.py` - Main training script
- `model_decoding_raw.py` - Model architecture
- `data_raw.py` - Data loading utilities
- `config.py` - Configuration management
- `util/` - Utility scripts for dataset preparation
- `scripts/` - Training and preparation scripts

## Model Architecture
The BrainTranslator model uses:
- BiLSTM encoder for EEG features
- Transformer layers for sequence modeling
- BART decoder for text generation

## Training Process
1. **Step 1**: Train EEG encoder (25 epochs)
2. **Step 2**: Fine-tune full model (25 epochs)

## Requirements
- Python 3.8+
- PyTorch 2.0+
- Transformers 4.0+
- CUDA-capable GPU (recommended)
