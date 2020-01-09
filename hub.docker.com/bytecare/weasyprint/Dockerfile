FROM ubuntu:xenial

RUN apt-get update && apt-get install -y \
    build-essential \
    python3-dev \
    python3-pip \
    python3-cffi \
    libcairo2 \
    libpango1.0-0 \
    libgdk-pixbuf2.0-0 \
    libffi-dev \
    shared-mime-info

RUN pip3 install --upgrade pip

RUN pip3 install WeasyPrint

RUN rm -rf /var/lib/apt/lists/*