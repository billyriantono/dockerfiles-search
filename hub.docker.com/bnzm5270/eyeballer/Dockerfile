FROM tensorflow/tensorflow:latest-gpu-py3

RUN apt install -y git && \
  mkdir /app && \
  git clone https://github.com/BishopFox/eyeballer.git /app && \
  cd /app && \
  pip3 install -r requirements-gpu.txt

