FROM tensorflow/tensorflow:1.11.0-gpu

RUN pip install pillow lxml jupyter matplotlib keras==2.2.4

RUN apt-get update && \
    apt-get install -y python-tk python-opencv ffmpeg \
    &&  rm -rf /var/lib/apt/lists/*
