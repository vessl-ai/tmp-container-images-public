# Images

VESSL container images for runs and workspaces.

## List of images

### CPU images

These images are based on [official Python images in Docker Hub](https://hub.docker.com/_/python).  
They include CPU versions of PyTorch and Tensorflow.

For more info, please [refer to `cpu/README.md`](cpu/README.md).

Image tags (not exhaustive):

* `quay.io/vessl-ai/python:3.9`
* `quay.io/vessl-ai/python:3.10`
* `quay.io/vessl-ai/python:3.11`

### NGC CUDA-based images

These images are based on NGC CUDA images: `nvcr.io/nvidia/cuda`.  
We provide images with just CUDA, or combined with PyTorch.

For more info, please [refer to `cuda/README.md`](cuda/README.md).

Image tags (not exhaustive):

* `quay.io/vessl-ai/cuda:12.1`
* `quay.io/vessl-ai/torch:2.3.1-cuda12.1`

### NGC Optimized Frameworks (deprecated)

> **NOTE**: Since July 2024, we are migrating to NGC CUDA-based images.  
> This means that future images will not be based on NGC PyTorch or Tensorflow images,
> but on a lighter image that contain a smaller set of libraries pre-installed.

Previous releases of VESSL container images are based on NGC PyTorch and Tensorflow images:
`nvcr.io/nvidia/pytorch` and `nvcr.io/nvidia/tensorflow`.
They contain more libraries out-of-the-box but are heavier and slower to pull.

For more info, please [refer to `deprecated-ngc/README.md`](deprecated-ngc/README.md).

Image tags (not exhaustive):

* `quay.io/vessl-ai/torch:2.3.0-cuda12.4-r5`
* `quay.io/vessl-ai/tensorflow:2.16.1-cuda12.5-r1`

## About images

### Image content

All images contain the following software packages:

* `curl`
* `git`
* `openssh-server`
* Jupyterlab (Python package)

Also, all images comes with the following, most commonly used Python packages in data science:

```
numpy, scipy, pandas, matplotlib, scikit-learn, opencv-python, seaborn, tqdm
```

### Image versioning scheme

You may find some image tags with suffixes `-r1`, `-r2`, etc.
These suffixes denote the revision number after changes in image content.  
In these cases, a "standard" image without the revision number is also available,
and is always equal to the latest revision.

For example, if the following image is available:

```
quay.io/vessl-ai/python:3.10-r14
```

then the following "standard" image is also available, and is always updated to point to
the latest revision of Python 3.10 images.

```
quay.io/vessl-ai/python:3.10
```

The **standard image** is enough for use in most cases, because:

* It is easier to read.
* Engineers in VESSL AI make sure that each image is reliable and compatible.
* Most of the image content stays the same on each revision release.

However, if you prefer to have a strictly reproducible environment across a long time,
you may pin and use a specific revision.