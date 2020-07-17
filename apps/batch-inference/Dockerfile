FROM rikorose/gcc-cmake as base

RUN apt-get update && apt-get install -y build-essential apt-utils \
    libfreetype6-dev \
    libfontconfig1-dev \
    wget \
    libfontconfig1 \
    fonts-liberation \
    tesseract-ocr \
    pdftk \
    xz-utils \
    libjpeg-dev \
    libopenjp2-7-dev

RUN wget https://poppler.freedesktop.org/poppler-data-0.4.9.tar.gz && \
    wget https://poppler.freedesktop.org/poppler-0.90.1.tar.xz && \
    tar xvf poppler-data-0.4.9.tar.gz && \
    tar xvf poppler-0.90.1.tar.xz && \
    cd poppler-data-0.4.9 && \
    make install && \
    cd .. && \
    cd poppler-0.90.1 && \
    mkdir build && \
    cd build && \
    cmake .. -DCMAKE_INSTALL_PREFIX=/usr && \
    make install && \
    cd ../.. && \
    rm -rf poppler-*

ARG PYTHON=python3.7

ENV LANG C.UTF-8

RUN apt-get install -y ${PYTHON}-dev

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN ${PYTHON} get-pip.py
RUN ln -sf /usr/bin/${PYTHON} /usr/local/bin/python3
RUN ln -sf /usr/local/bin/pip /usr/local/bin/pip3

RUN pip3 --no-cache-dir install --upgrade psutil\
    pip \
    setuptools \
    Cython

RUN ln -s $(which ${PYTHON}) /usr/local/bin/python

RUN pip3 install --upgrade python-poppler

RUN pip3 install flask \
    pillow \
    tensorflow==2.0.0b1 \
    flask \
    opencv-python \
    scikit-image \
    pytesseract \
    keras \
    luigi \
    pygtrie

RUN pip3 install lxml pandas PyPDF2 camelot-py
RUN pip3 install requests
RUN pip3 install pdf2image