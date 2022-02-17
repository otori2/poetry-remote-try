ARG CUDA_VERSION=11.4.0
FROM nvidia/cuda:${CUDA_VERSION}-runtime-ubuntu20.04
ENV DEBIAN_FRONTEND=noninteractive

ARG PYTHON_VERSION=3.9.9

RUN apt-get -y update && \
    apt-get -y install wget curl libboost-all-dev cmake git libffi-dev libbz2-dev libreadline-dev libsqlite3-dev libssl-dev liblzma-dev build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Python
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz 2>/dev/null 1>/dev/null
RUN tar xJf Python-${PYTHON_VERSION}.tar.xz && \
    cd Python-${PYTHON_VERSION} && \
    ./configure && \
    make && \
    make install
RUN python3 -m pip install --upgrade pip
RUN cd /usr/local/bin && \
    ln -s python3 python

WORKDIR /workspace

COPY poetry.lock* pyproject.toml ./

RUN pip install poetry
RUN poetry config virtualenvs.create false && \
    poetry install

# Install PyTorch
# RUN pip3 install torch==1.10.2+cu113 torchvision==0.11.3+cu113 torchaudio==0.10.2+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
