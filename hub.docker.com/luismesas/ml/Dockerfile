FROM tensorflow/tensorflow:latest-gpu-py3

ADD requirements.txt .
RUN pip install -r requirements.txt
RUN apt update && apt install -y libsm6 libxext6 libxrender1
# libfontconfig1
CMD ["nvidia-smi"]
