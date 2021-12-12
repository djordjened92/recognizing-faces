# Blood relation detection

This repository is educational purposes project which refers to [Northeastern SMILE Lab](https://web.northeastern.edu/smilelab/)
[Recognizing Faces in the Wild competition](https://www.kaggle.com/c/recognizing-faces-in-the-wild). The goal is to determine if 
two people are blood-related based solely on images of their faces. There is a training set of images grouped by person and by their families, and .csv file with pairs of relatives. Images are not provided in repository, they are accessible through Kaggle API using
command _kaggle competitions download -c recognizing-faces-in-the-wild_ (more information about kaggle API is [here](https://github.com/Kaggle/kaggle-api)).

Positive pairs of images are initially provided, but for training and testing purposes, negative pairs of people who are not relatives are generated additionaly.

This project examines several model selection options, among them [VGGFace](https://github.com/rcmalli/keras-vggface) ResNet50 pretrained model, as the most popular in the competition's top scored notebooks.

## 1. Introduction
[Northeastern SMILE Lab](https://web.northeastern.edu/smilelab/)
[Recognizing Faces in the Wild competition](https://www.kaggle.com/c/recognizing-faces-in-the-wild) is the well known Kaggle competition related to a task of the kinship verification based on the face images only. This project is an attempt to approach the problem with classic metric learning techniques including some customization.

Top-score leaderboard notebooks mostly use Siamese Network models for the feature extraction, then different comparison calculations of two outputs(<img src="https://render.githubusercontent.com/render/math?math=|X_1 - X_2|">, <img src="https://render.githubusercontent.com/render/math?math=X_1 %2B X_2">, <img src="https://render.githubusercontent.com/render/math?math=X_1^2 - X_2^2">, <img src="https://render.githubusercontent.com/render/math?math=(X_1 - X_2)^2">, ...) which are concatenated and merged into one-node fully connected layer with sigmoid function output. In that way the whole problem is reduced to the binary classification with crossentropy loss. Widely used base model(feature extractor) is pretrained [VGGFace](https://github.com/rcmalli/keras-vggface) and [FaceNet](https://github.com/davidsandberg/facenet) model. They are usually fine-tuned with excluding only few last layers. Solutions which achieve the best results use ensembles of 10, 20 or even more than 30 models with this model pattern. One of the notebook example is the [winning one](https://www.kaggle.com/mattemilio/smile-best-who-smile-last).

This project is based on the Siamese Network architecture also, but using contrastive loss with learnable margin. The same pretrained models are used as based models, but with this approach it is sufficient to fine-tune only a small part of the network. Obtained private score ([ROC AUC score](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) at the [private leaderboard](https://www.kaggle.com/c/recognizing-faces-in-the-wild/leaderboard)) **0.86** (the best score is 0.923) is a decent baseline for the further improvement.

## 2. Dataset
## 3. Model
## 4. Result