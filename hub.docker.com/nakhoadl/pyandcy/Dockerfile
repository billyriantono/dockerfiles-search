FROM python:3.6.9-slim-stretch 

ENV PYTHONUNBUFFERED 1

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Cache in file use for build sub images.
RUN echo "build-essential \
          libbz2-dev \
          libpq-dev \
          libjpeg62-turbo-dev \
          libtiff-dev \
          libfreetype6 \
          libfreetype6-dev \
          libwebp-dev \
          libopenjp2-7-dev \
          linux-headers-4.9 \
          libxml2-dev \
          libxslt-dev \
          cmake \
          tcl-dev \
          xz-utils \
          zlib1g-dev \
          libssl-dev \
          libncurses5-dev \
          libsqlite3-dev \
          libreadline-dev \
          libtk8.5 \
          libgdm-dev \
          libdb4o-cil-dev \
          libpcap-dev \
          git \
          wget \
          curl \
          libpulse-dev \
          antiword \
          tesseract-ocr \
          swig" >> .build_packages

ENV APT_PACKAGES="ca-certificates \
                  openssl \
                  bzip2 \
                  libpq5 \
                  sqlite3 \
                  bash \
                  fonts-noto \
                  libpng16-16 \
                  libfreetype6 \
                  libjpeg62-turbo \
                  libgomp1" \
    PIP_PACKAGES="pyyaml \
                  pymkl \
                  cffi \
                  h5py \
                  requests \
                  pillow \
                  graphviz \
                  pandas \
                  scipy \
                  scikit-learn \
                  seaborn \
                  matplotlib \
                  pydot \
                  sympy \
                  sumy \
                  spacy \
                  gensim \
                  textblob \
                  xgboost \
                  tensorflow \
                  keras \
                  https://download.pytorch.org/whl/cpu/torch-1.1.0-cp36-cp36m-linux_x86_64.whl \
                  https://download.pytorch.org/whl/cpu/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl \
                  mxnet-mkl" \
    LANG=C.UTF-8

RUN set -ex; \
    apt-get update -y; \
    apt-get upgrade -y; \
    apt-get install -y $(cat .build_packages); \
    apt-get install -y --no-install-recommends --fix-missing ${APT_PACKAGES};

RUN pip install -U -V pip; \
    pip install -U -v setuptools wheel Cython numpy; \
    pip install -U -v ${PIP_PACKAGES}; \
    python -m nltk.downloader -d /nltk_data all; \
    python -m spacy download en; \
    python -m spacy download en_core_web_sm; \
    python -m textblob.download_corpora

ENTRYPOINT [ "/bin/bash" ]
