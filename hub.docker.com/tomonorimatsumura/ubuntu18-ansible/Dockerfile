FROM ubuntu:latest

RUN apt update -y && \
    apt install -y language-pack-ja-base language-pack-ja && \
    apt install -y software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt update -y && \
    apt install -y curl python-dev git && \
    curl "https://bootstrap.pypa.io/get-pip.py" -o "/tmp/get-pip.py" && \
    python /tmp/get-pip.py && \
    pip install --upgrade pip && pip install --upgrade setuptools && \
    pip install ansible && \
    pip install ansible-lint

ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"
