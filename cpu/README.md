# CPU images

These images are based on [official Python images in Docker Hub](https://hub.docker.com/_/python).
They include CPU versions of PyTorch and Tensorflow.

Image tags (not exhaustive):

* `quay.io/vessl-ai/python:3.9`
* `quay.io/vessl-ai/python:3.10`
* `quay.io/vessl-ai/python:3.11`

Dockerfile is located here in `cpu/`.

Dockerfile parameters (with default values):

* `PY_VERSION`: Python version to install.
    * default: `3.10`