FROM python:3-alpine
RUN ["apk", "add", "--no-cache", "gcc", "musl-dev", "python3-dev", "build-base"]
COPY requirements.txt /
RUN ["pip", "install", "--no-cache-dir", "-r", "requirements.txt"]