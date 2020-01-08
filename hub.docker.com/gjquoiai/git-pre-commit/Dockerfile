FROM python:3-alpine

RUN apk add --no-cache \
    git \
    build-base

WORKDIR /pre-commit

RUN pip install --no-cache-dir -i https://pypi.tuna.tsinghua.edu.cn/simple \
    pre-commit

COPY .pre-commit-config-for-build.yaml .pre-commit-config.yaml

RUN git init . && \
    cat .pre-commit-config.yaml && \
    pre-commit run
