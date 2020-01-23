FROM continuumio/miniconda3:latest

RUN apt update && apt install -y build-essential cmake git && pip install --upgrade pip && pip install virtualenv awscli && virtualenv /face-recognition && /face-recognition/bin/pip install dlib numpy boto3 requests pillow


