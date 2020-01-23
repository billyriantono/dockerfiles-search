FROM python:3.6
MAINTAINER Ivan Miniailenko <discrete.west@gmail.com>

RUN pip install --no-cache-dir tensorflow

VOLUME /tflog

EXPOSE 6006

CMD ["python3", "-m", "tensorflow.tensorboard", "--logdir=/tflog"]