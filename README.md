

# Convolutional Gated Autoencoder for Learning Transposition-invariant Features from Audio

PyTorch implementation of the sequential Gated Autoencoder proposed in 

*Learning Transposition-Invariant Interval Features from Symbolic Music and 
Audio*<br/>
Stefan Lattner¹², Maarten Grachten¹, Gerhard Widmer¹, 2018<br/>

*Audio-to-Score Alignment using Transposition-Invariant Features*<br/>
Andreas Arzt¹, Stefan Lattner¹², 2018<br/>

*¹Institute of Computational Perception, JKU Linz*<br/> 
*²Sony CSL Paris*<br/>

The method introduced in the papers is based on n-grams for learning the intervals between input and target, whereas the 
implementation provided here employs convolution in time.

Pre-trained model parameters can be used as described [here](#convert-audio-files-to-invariant-features). However, we encourage the user
to train the model on problem-specific data, and to experiment with different 
training settings herself.

### Outline ###

* Prerequisites
* Training
* Convert audio

### Prerequisites ###

* [PyTorch](http://www.pytorch.org)
* Librosa
* Matplotlib
* Pillow
* Numpy

**Install PyTorch** following [this link](http://www.pytorch.org).

To install (update) all other requirements using **Conda**, run:
```
  conda install --yes --file requirements.txt
```
To install (update) all other requirements using **pip**, run:
```
  pip install -r requirements.txt
```

## Training

1. **Create a text file** which lists audio files to use for training, e.g.:

*filelist.txt:*
```
data/audio1.wav
data/audio2.wav
data/audio3.wav
```
We recommend ~2-3 hours of music for training with the default parameters.

2. **Start training** using the following command
(choose a *run_keyword*, add `--help` to list all parameters):
```
  python train.py filelist.txt run_keyword
```
Note that file preprocessing will be cached. Thus, when changing data-related *parameters* or when modifying the *filelist.txt* file, use the flag `--refresh-cache`.
An experiment folder `output/run_keyword` will be created, where all files regarding the experiment (including plots and parameters of the trained network) will be placed.

## Convert audio files to invariant features

1. **Create a text file** (e.g. filelist.txt) which lists audio files to convert (see Section [Training](#training)).
2. **Convert files**, run (using the same *run_keyword* as in the training):
```
  python convert.py filelist.txt run_keyword
```
In order to **use pre-trained parameters**, run
```
  python convert.py filelist.txt pretrained
```
The converted files will be saved (bz2 compressed pickle) in the experiment folder `output/run_keyword`.
A method to load the compressed files as numpy arrays can be found in cqt.py -> load_pyc_bz(filename)

## Acknowledgements
This research was supported by the EU FP7 (project Lrn2Cre8, FET grant number 610859), and the European Research Council (project CON ESPRESSIONE, ERC grant number 670035).
