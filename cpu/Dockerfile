ARG PY_VERSION=3.10
FROM python:${PY_VERSION}-slim-buster

ARG DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1 \
    PATH=/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LANG=C.UTF-8 \
    SHELL=/bin/bash
ENV MXNET_VERSION 1.9.1
ENV TF_VERSION 2.12.0
ENV TF_HUB 0.13.0
ENV TORCH_VERSION 1.13.1
ENV TORCHVISION_VERSION 0.14.1

USER root

RUN apt-get update && \
    apt-get install -yq --no-install-recommends \
        build-essential \
        ca-certificates curl \
        gcc g++ git git-core \
        libgeos-dev libgeos++-dev libglib2.0-0 libgl1-mesa-glx libmpdec2 libproj-dev libsndfile1 libssl-dev \
        mime-support \
        openssh-server \
        sudo \
        vim jq tmux \
        unzip zip \
        wget \
        libpython${PY_VERSION}-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir --no-compile -U pip && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl

# Install data science dependencies
COPY requirements.datascience.txt requirements.txt
RUN pip install --no-cache-dir --no-compile -r requirements.txt && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl && \
    rm -f requirements.txt

# Install CLI
RUN pip install --no-cache-dir --no-compile vessl && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl

RUN pip install --no-cache-dir --no-compile \
    mxnet==$MXNET_VERSION \
    tensorflow-cpu==$TF_VERSION \
    tensorboard \
    torch==${TORCH_VERSION}+cpu \
    torchvision==${TORCHVISION_VERSION}+cpu \
    keras \
    tensorflow-hub==$TF_HUB tf2onnx \
    --extra-index-url https://download.pytorch.org/whl/cpu && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl

RUN pip install --no-cache-dir --no-compile \
    jupyterlab jupyterlab-git ipywidgets && \
    rm -rf /root/.cache && \
    rm -f /tmp/*.whl

# Install git-lfs
RUN apt-get update && \
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
    apt-get install git-lfs && \
    git lfs install && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY start-notebook.sh /usr/local/bin/
ENTRYPOINT ["bash"]
CMD ["start-notebook.sh"]
