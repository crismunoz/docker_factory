ARG UBUNTU_VERSION=16.04
FROM ubuntu:${UBUNTU_VERSION} as base

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        pkg-config \
        software-properties-common \
        unzip \
        wget

RUN apt-get update \
        && apt-get install -y libsm6 libxext6 libxrender-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

ARG PYTHON=python3.7

ENV LANG C.UTF-8

RUN add-apt-repository ppa:deadsnakes/ppa && apt-get update && apt-get install -y ${PYTHON}

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN ${PYTHON} get-pip.py
RUN ln -sf /usr/bin/${PYTHON} /usr/local/bin/python3
RUN ln -sf /usr/local/bin/pip /usr/local/bin/pip3

RUN pip3 --no-cache-dir install --upgrade \
    pip \
    setuptools

RUN ln -s $(which ${PYTHON}) /usr/local/bin/python

ARG TF_PACKAGE=tensorflow==1.13.2
RUN pip3 install --upgrade ${TF_PACKAGE}