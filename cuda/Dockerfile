ARG BASE_IMAGE_VERSION=12.1.1-cudnn8-devel-ubuntu22.04
FROM nvcr.io/nvidia/cuda:${BASE_IMAGE_VERSION} AS cuda
ARG PY_VERSION=3.10

ENV DEBIAN_FRONTEND=noninteractive
ENTRYPOINT ["/bin/bash"]
CMD []

# Install Python
RUN apt-get update && \
    apt-get install -yq \
        # Install basic dependencies here
        git openssh-server curl software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get install -yq python${PY_VERSION} python${PY_VERSION}-venv binutils binfmt-support && \
    ln -s python3 /usr/bin/python && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

# Install Pip
RUN curl -sSL https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python3 get-pip.py --no-cache-dir --no-compile && \
    rm get-pip.py

# Install data science dependencies
COPY requirements.datascience.txt requirements.txt
RUN pip install --no-cache-dir --no-compile -r requirements.txt && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl && \
    rm -f requirements.txt

# Install VESSL SDK/CLI
RUN pip3 install --no-cache-dir --no-compile --disable-pip-version-check \
        vessl

# Install Jupyter
RUN pip3 install --no-cache-dir --no-compile --disable-pip-version-check \
    jupyterlab jupyterlab-git ipywidgets

FROM cuda AS torch
ARG TORCH_VERSION=2.3.1
ARG TORCH_INDEX=cu118
RUN pip3 install --no-cache-dir --no-compile --disable-pip-version-check \
        "torch~="${TORCH_VERSION} torchvision torchaudio \
        --index-url https://download.pytorch.org/whl/${TORCH_INDEX}
