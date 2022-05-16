ARG nvidia_cuda_version=11.4.1-cudnn8-runtime-ubuntu20.04
FROM nvidia/cuda:${nvidia_cuda_version}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ARG REQUIREMENTS_TXT=requirements.txt

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt update && apt -y full-upgrade \
    && apt -y install build-essential libgirepository1.0-dev gcc libcairo2-dev python3-dev gir1.2-gtk-3.0 pkg-config swig \
    && apt -y install --no-install-recommends apt-utils dialog 2>&1 \
    && apt -y install git iproute2 procps lsb-release \
    && apt -y install libcairo2 libcairo2-dev \
    && apt -y install libgl1 \
    && apt -y install \
    python3.8 \
    python3-pip \
    python3-venv \
    python3.8-venv \
    && apt -y install python3.8-dev \
    && python3.8 -m pip install -U pip \
    && python3.8 -m pip install setuptools wheel \
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt -y install sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
    
RUN rm -rf /var/lib/apt/lists/*
    
COPY $REQUIREMENTS_TXT /tmp/
RUN python3.8 -m venv /home/vscode/.venv/instagan
RUN /home/vscode/.venv/instagan/bin/python -m pip install -U pip
RUN /home/vscode/.venv/instagan/bin/pip install --no-cache-dir -r /tmp/$REQUIREMENTS_TXT
