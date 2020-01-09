FROM python:3.7-slim

RUN apt-get update \ 
 && apt-get install -y \
    gcc \
    g++ \
 && pip install "https://github.com/megagonlabs/ginza/releases/download/latest/ginza-latest.tar.gz" \
 && apt-get clean \
 && rm --recursive --force /var/lib/apt/lists/*
