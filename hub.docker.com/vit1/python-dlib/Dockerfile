FROM python:3.7

RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    libopenblas-dev \
    liblapack-dev \
  && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir -U pip && pip install --no-cache-dir dlib
