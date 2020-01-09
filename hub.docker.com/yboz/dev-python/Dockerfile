FROM yboz/graphical:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y && apt install -y \
    python3.5 \
    python3-pydbus \
    python3-gi \
    python3-pip && \
    python3 -m pip install msgpack-python fluent-logger pylint

USER dev
WORKDIR /home/dev
