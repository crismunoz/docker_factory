ARG DRIVER=gpu
FROM tensorflow/tensorflow:2.3.0-gpu-jupyter as base
RUN apt-get update \
        && apt-get install -y wget libsm6 libxext6 libxrender-dev libgl1-mesa-glx \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN pip3 --no-cache-dir install flask \
    pillow \
    opencv-python \
    scikit-image \
    pytesseract \
    pandas \
    tqdm \
    spacy \
    nltk \
    jupyter \
    sklearn

RUN pip3 --no-cache-dir install Keras-Applications \
    imgaug \
    MNN \
    onnxruntime \
    optimizer_type
   
RUN pip3 --no-cache-dir install --upgrade tensorflow-model-optimization

RUN mkdir -p /tmp/openmpi && \
    cd /tmp/openmpi && \
    wget https://www.open-mpi.org/software/ompi/v4.0/downloads/openmpi-4.0.4.tar.gz && \
    tar zxf openmpi-4.0.4.tar.gz && \
    cd openmpi-4.0.4 && \
    ./configure --enable-orterun-prefix-by-default --with-cuda && \
    make -j $(nproc) all && \
    make install && \
    ldconfig && \
    rm -rf /tmp/openmpi

RUN ldconfig /usr/local/cuda/targets/x86_64-linux/lib/stubs && \
    HOROVOD_GPU_OPERATIONS=NCCL HOROVOD_WITH_TENSORFLOW=1 HOROVOD_WITH_PYTORCH=1 HOROVOD_WITH_MXNET=1 \
         pip install --no-cache-dir horovod && \
    ldconfig

RUN apt-get install -y --no-install-recommends openssh-client openssh-server && \
    mkdir -p /var/run/sshd

RUN cat /etc/ssh/ssh_config | grep -v StrictHostKeyChecking > /etc/ssh/ssh_config.new && \
    echo "    StrictHostKeyChecking no" >> /etc/ssh/ssh_config.new && \
    mv /etc/ssh/ssh_config.new /etc/ssh/ssh_config

RUN apt-get install -y --no-install-recommends subversion && \
    svn checkout https://github.com/horovod/horovod/trunk/examples && \
    rm -rf /examples/.svn
