# Docker file for the nirs_demo_app plugin app

FROM nvidia/cuda:9.0-devel-ubuntu16.04 as builder

WORKDIR /usr/src/mcx/build
COPY ["mcx", "/usr/src/mcx"]
RUN apt-get update && \
    apt-get install -y --no-install-recommends wget python3 python3-pip && \
    wget -q https://cmake.org/files/v3.12/cmake-3.12.3-Linux-x86_64.sh  && \
    mkdir /usr/cmake && \
    sh cmake-3.12.3-Linux-x86_64.sh --skip-license --prefix=/usr/cmake && \
    ln -s /usr/cmake/bin/cmake /usr/bin/cmake && \
    pip3 install setuptools wheel && \
    cmake .. && \
    make pymcx

FROM python:3-slim
MAINTAINER fnndsc "dev@babymri.org"

LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility

ENV APPROOT="/usr/src/nirs_demo_app"  VERSION="0.1"
COPY ["nirs_demo_app", "${APPROOT}"]
COPY ["requirements.txt", "${APPROOT}"]
COPY --from=builder ["/usr/src/mcx/build/pymcx", "${APPROOT}/pymcx"]

WORKDIR $APPROOT

RUN apt-get update && \
    apt-get install -y --no-install-recommends libgomp1 && \
    pip3 install --no-cache-dir -r requirements.txt && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["python3"]
CMD ["nirs_demo_app.py", "--json"]
