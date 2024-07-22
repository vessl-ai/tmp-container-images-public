# NGC Optimized Frameworks (deprecated)

> **NOTE**: Since July 2024, we are migrating to NGC CUDA-based images.
> This means that future images will not be based on NGC PyTorch or Tensorflow images,
> but on a lighter image that contain a smaller set of libraries pre-installed.

NVIDIA Optimized Frameworks images, also known as "NGC" images when the context is clear, contain
various up-to-date libraries for deep learning workloads and others, including CUDA, cuBLAS,
cuDNN, NCCL, and OpenMPI. Some versions also include specific deep learning framewors, such as
PyTorch or Tensorflow.

Previous releases of VESSL container images are based on NGC PyTorch and Tensorflow images:

* `nvcr.io/nvidia/pytorch`
* `nvcr.io/nvidia/tensorflow`

Please refer to their release notes for more detail.

- [Release Note: NGC PyTorch Images](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/index.html)
- [Release Note: NGC Tensorflow Images](https://docs.nvidia.com/deeplearning/frameworks/tensorflow-release-notes/index.html)

Image tags (not exhaustive):

* `quay.io/vessl-ai/torch:1.14.0-cuda12.0`
* `quay.io/vessl-ai/torch:2.1.0-cuda12.2`
* `quay.io/vessl-ai/torch:2.2.0-cuda12.3`
* `quay.io/vessl-ai/torch:2.3.0-cuda12.4`
* `quay.io/vessl-ai/torch:2.4.0-cuda12.4`
* `quay.io/vessl-ai/tensorflow:2.14.0-cuda12.3`
* `quay.io/vessl-ai/tensorflow:2.15.0-cuda12.4`
* `quay.io/vessl-ai/tensorflow:2.16.1-cuda12.5`