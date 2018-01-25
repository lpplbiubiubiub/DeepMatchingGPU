# DeepMatchingGPU
A modified version of [DeepMatchingGPU](https://github.com/WIStudent/DeepMatchingGPU) that is compatible with [Caffe 1.0](https://github.com/BVLC/caffe) and Ubuntu 16.10.

The original version need cmake-gui or g++-5 or gcc-5, and after test, I think it's unnecessary. U just need a caffe 1.0.

Here is it what change i made:
1.specific CAFFEDIR as /your_caffe_dir/.release_build/ (.release_build is generated when you compile caffe)


2.make some change on gpudm.swig like move the defination of google's namespace


3.add CUDALIB in gpudm.swig(it depends)


ATTENTION: version of protobuf should be 2.5
