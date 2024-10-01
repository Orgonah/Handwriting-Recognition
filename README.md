# Handwriting-Recognition

This project implements a handwriting recognition system using the IAM Dataset and Keras. The model is trained to recognize variable-length sequences of handwritten text from images.

## Data Collection
The dataset can be collected and extracted using the following commands:

```bash
wget -q https://github.com/sayakpaul/Handwriting-Recognizer-in-Keras/releases/download/v1.0.0/IAM_Words.zip
unzip -qq IAM_Words.zip

mkdir data
mkdir data/words
tar -xf IAM_Words/words.tgz -C data/words
mv IAM_Words/words.txt data
```

## Model Architecture
The model uses a combination of convolutional layers and bidirectional LSTMs, followed by a Connectionist Temporal Classification (CTC) loss layer. It performs the following steps:

- Extracts features from images using convolutional layers
- Processes the features using bidirectional LSTM layers for sequence learning
- Computes the CTC loss for variable-length output sequences

## Data Preprocessing
- The dataset is split into training (90%), validation (5%), and test (5%) sets.
- Images are resized without distortion and padded if necessary to maintain aspect ratio.
- Labels are processed at the character level using StringLookup layers for character-to-integer mapping.

## Training
The model is trained using the Adam optimizer and CTC loss function. The following key hyperparameters are used:

- Batch size: 64
- Image size: 128x32
- Padding token: 99

## Evaluation
The evaluation metric is Edit Distance, which measures the number of insertions, deletions, and substitutions required to transform the predicted sequence into the target sequence. A custom callback monitors the Edit Distance during training.