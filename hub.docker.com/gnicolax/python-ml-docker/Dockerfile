FROM python:3-alpine

ENV PYTHONUNBUFFERED=1

RUN apk update && \
    apk add --no-cache \
        libffi-dev \
        openblas-dev \
        cython \
        freetype-dev \
      	llvm8-dev \
        nano \
        tmux \
        build-base && \
    pip install --no-cache-dir cython && \
    pip install --no-cache-dir numpy && \
    pip install --no-cache-dir pandas && \
    pip install --no-cache-dir scipy && \
    pip install --no-cache-dir scikit-learn && \
    pip install --no-cache-dir matplotlib && \
    pip install --no-cache-dir pyod && \
    pip install --no-cache-dir elasticsearch
