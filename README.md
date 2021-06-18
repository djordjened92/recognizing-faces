# Blood relation detection using FaceNet

This repository is educational purposes project which refers to [Northeastern SMILE Lab](https://web.northeastern.edu/smilelab/)
[Recognizing Faces in the Wild competition](https://www.kaggle.com/c/recognizing-faces-in-the-wild). The goal is to determine if 
two people are blood-related based solely on images of their faces. There is a training set of images grouped by person and by their families, and .csv file with pairs of relatives. Images are not provided in repository, they are accessible through Kaggle API using
command _kaggle competitions download -c recognizing-faces-in-the-wild_ (more information about kaggle API is [here](https://github.com/Kaggle/kaggle-api)).

So this task is a way to try out [FaceNet: A Unified Embedding for Face Recognition and Clustering](https://arxiv.org/pdf/1503.03832.pdf),
since the main problem is basicaly face verification for people who are blood-related.

Positive pairs of images are initially provided, but for training and testing purposes, negative pairs of people who are not relatives are generated additionaly. Basically, model is Siamese Network with contrastive loss based on Euclidian distance of outputs (see [paper](http://yann.lecun.com/exdb/publis/pdf/chopra-05.pdf) for more details).
Hence, the input to the whole system is a pair of images and a label, where images pass through two identical networks and one cost module. Model contains two submodels, first one is pretrained FaceNet deep convolutional neural network and the second one is a trainable MLP.

Face embeddings are extracted using pretrained model from [keras-facenet](https://pypi.org/project/keras-facenet/) package, which is actually a wrapper around https://github.com/davidsandberg/facenet. Embeddings are stored in **data** directory.
