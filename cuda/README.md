# NGC CUDA-based images

These images are based on NGC CUDA images: `nvcr.io/nvidia/cuda`, which contain a variety
of Linux images with CUDA runtime pre-installed. Among those, we use the "`devel`" version,
based on Ubuntu, that also has cuDNN bundled.

We provide:

* CUDA images (that has only CUDA runtime and Python),
* PyTorch images (that has PyTorch pre-installed)

> **NOTE: About CUDA version discrepancies**  
>
> PyTorch wheels are pre-built with a specific set of CUDA versions, and those versions of
> CUDA libraries are installed as Python dependencies alongside PyTorch.
> Thus, **PyTorch will not use the CUDA libraries installed in the base NGC CUDA image**.  
>
> Although we try to keep the versions of two CUDA libraries (one in the base image, another
> in Python packages) close, some of them might have discrepancies, which may lead to unexpected
> behavior when you are running certain CUDA workloads outside PyTorch context.

Image tags (not exhaustive):

* `quay.io/vessl-ai/cuda:12.1`
* `quay.io/vessl-ai/torch:2.3.1-cuda12.1`

This Dockerfile has two build stages, namely `cuda` and `torch`. The latter builds upon the former.

Dockerfile parameters (with default values):

* `BASE_IMAGE_VERSION`: Tag for the base image of `nvcr.io/nvidia/cuda`.
    * Default: `12.1.1-cudnn8-devel-ubuntu22.04`
* `PY_VERSION`: Python version to install.
    * Default: `3.10`
* `TORCH_VERSION`: Torch version to install.
    * Ignored if build stage is not `torch`.
    * Default: `2.3.1`
* `TORCH_INDEX`: CUDA version for PyTorch installation.
    * This does not have to be equal to base image's CUDA version; see above note.
    * Ignored if build stage is not `torch`.
    * Default: `cu121`
