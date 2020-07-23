ARG DRIVER=gpu
FROM strink/tensorflow-${DRIVER}:1.14.0-py3.7 as base
RUN apt-get update \
        && apt-get install -y libsm6 libxext6 libxrender-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN pip3 --no-cache-dir install flask \
    pillow \
    opencv-python \
    scikit-image \
    pytesseract \
    pandas \
    tqdm \
    keras==2.2.5