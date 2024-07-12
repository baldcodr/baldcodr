---
title: "A complete guide to installing TensorFlow on M1 Mac with GPU capability"
seoTitle: "a-complete-guide-to-installing-tensorflow-on-m1-mac-with-gpu"
seoDescription: "how to set up your Mac M1 for your deep learning project using TensorFlow"
datePublished: Thu Mar 17 2022 07:32:07 GMT+0000 (Coordinated Universal Time)
cuid: cl0uocjq60059djnv46xvfrdd
slug: a-complete-guide-to-installing-tensorflow-on-m1-mac-with-gpu-capability
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/Jx-UX9zVdKk/upload/v1647501509921/2AlqK2fT_.jpeg
tags: apple, machine-learning, tensorflow, data-analysis, macos

---

One of the major innovations that come with the new Mac ARM M1-based machines is CPU, GPU and deep learning hardware support on a single chip, unlike the older-intel based chips. This article will discuss how to set up your Mac M1 for your deep learning project using TensorFlow. We will also install several other deep learning libraries.

In other to access the new M1 chip from python, you must install a special distribution of python called Miniforge. Since the M1 uses a different architecture than Intel, with Miniforge you can access the GPU capabilities embedded in this new chip. Let's get started.

\*\*NB: \*\* Before you go ahead with this, ensure you have properly uninstalled anaconda from your machine if you have it previously installed. [Here](https://setapp.com/how-to/uninstall-anaconda-on-mac) is a guide on how to uninstall anaconda using [CleanMyMac X](https://setapp.com/how-to/uninstall-anaconda-on-mac) or using the anaconda-clean package.

## Install Miniforge

Using Homebrew(a package manager for Mac similar to apt-get for Linux).

```python
brew install miniforge
```

OR

Download and install [Miniforge3](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh) by running the following command on your terminal:

```python
chmod +x ~/Downloads/Miniforge3-MacOSX-arm64.sh
sh ~/Downloads/Miniforge3-MacOSX-arm64.sh
source ~/miniforge3/bin/activate
```

## Add Miniforge to path

```python
conda init
```

This will add miniforge to your bash profile(default). You can use the --all flag to include all shell types.

## Create the TensorFlow environment and install Jupyter notebook

tf-apple-m1.yml script

```python
name: tf_env
 
dependencies:
    - python=3.9
    - pip>=22.0
    - jupyter
    - apple::tensorflow-deps
    - scikit-learn
    - scipy
    - numpy
    - pandas
    - pandas-datareader
    - matplotlib
    - pillow
    - tqdm
    - requests
    - h5py
    - pyyaml
    - flask
    - boto3
    - pip:
        - tensorflow-macos
        - tensorflow-metal
        - bayesian-optimization
        - gym
```

Let's create a new virtual environment using the tf-apple-m1.yml script above. Save the script to the same directory you are running the command from.

```python
#first deactivate the base environment which is currently running
conda deactivate 

#create new virtual environment
conda env create -f tf-apple-m1.yml -n tf_env

#activate the new environment
conda activate tf_env

#Install Jupiter Notebook
conda install -y jupyter nb_conda

#This registers your new tf_env environment and allows you to switch to it from Jupiter Notebook
python -m ipykernel install --user --name tf_env --display-name "Python 3.9 (tf_env)"
```

## Test your new environment for Tensorflow and other dependencies.

```python
#start up jupyter notebook
jupyter notebook
```

Run the following command in your notebook, ensure that your kernel is showing "Python 3.9 (tf\_env)".

```python
import sys
import pandas as pd
import sklearn as sk
import tensorflow.keras as ks
import tensorflow as tf

print(f"Tensor Flow Version: {tf.__version__}")
print(f"Keras Version: {ks.__version__}")
print()
print(f"Python {sys.version}")
print(f"Pandas {pd.__version__}")
print(f"Scikit-Learn {sk.__version__}")
gpu = len(tf.config.list_physical_devices('GPU'))>0
print("GPU is", "available" if gpu else "NOT AVAILABLE")
```

## CONCLUSION

Here we discussed how to install miniforge and miniconda, a lightweight alternative to anaconda for managing data science libraries on the M1 Mac OS. We have gone through the process of setting up our machine for deep learning by installing Tensorflow and other ML libraries.