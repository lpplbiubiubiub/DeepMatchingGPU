# Compiling DeepMatching's GPU version on Ubuntu 16.10
[DeepMatching](http://lear.inrialpes.fr/src/deepmatching/) is an algorithm that finds corresponding points in two images. Its GPU implementation was written for Fedora 21, which makes things a bit more difficult if you want to run it on an Ubuntu system. This document contains step-by-step instructions on how to get DeepMatching running on Ubuntu 16.10. I only tested it with Ubuntu 16.10, let me know if it works with previous versions too.


## Compiling Caffe
Before compiling Caffe we need to make sure all its dependencies are installed. From the [installation guide for Ubuntu 16.04/15.10](https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide):
```sh
sudo apt-get install build-essential cmake git pkg-config

sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler

sudo apt-get install libatlas-base-dev

sudo apt-get install --no-install-recommends libboost-all-dev

sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

# (Python general)
sudo apt-get install python-pip

# (Python 2.7 development files)
sudo apt-get install python-dev
sudo apt-get install python-numpy python-scipy

# (or, Python 3.5 development files)
sudo apt-get install python3-dev
sudo apt-get install python3-numpy python3-scipy
```
You also need to install Nvidia CUDA. All you need to do is install the packages `nvidia-cuda-dev` and `nvidia-cuda-toolkit`
```sh
sudo apt-get install nvidia-cuda-dev nvidia-cuda-toolkit
```
To install all python dependencies, extract the `caffe.zip` folder, navigate to `caffe\python` and execute
```sh
cd caffe/python
for req in $(cat requirements.txt); do pip install $req; done
```
To complie caffe
```sh
cd caffe
make all -j8
```
Now we can start compiling DeepMatching.
## Compiling DeepMatching
Before we can compile DeepMatching, we need to install the packages `python-matplotlib` and `swig`.
```
sudo apt-get install python-matplotlib swig
```
The Makefile that comes with the original DeepMatching isn't really compatible with Ubuntu, it contains many paths that don't work on Ubuntu. That's why I wrote my own Makefile.

The only thing you need to do is set `CAFFE_DIR` to the location of the `install` folder that was created during the compiling of Caffe. To compile, simply run `make all`. To test if DeepMatching runs correctly, execute
```
python deep_matching_gpu.py liberty1.png liberty2.png -v -viz corres
```
For more information about DeepMatching, look into the included `ORIGINAL_README.txt` file.
