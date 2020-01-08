FROM python:3.5-stretch

RUN pip install flask wget
RUN pip install pandas numpy
RUN pip install Pillow scp
RUN pip install pypinyin
RUN pip install regex requests jieba arrow pyYaml matplotlib opencv-python
RUN pip install tensorflow==1.13.1

RUN apt-get update
RUN apt-get -y install cmake protobuf-compiler

WORKDIR /usr/local/lib/python3.5/site-packages/tensorflow
RUN wget https://github.com/tensorflow/models/archive/master.zip
RUN unzip master.zip

WORKDIR /usr/local/lib/python3.5/site-packages/tensorflow/models-master/research

RUN protoc object_detection/protos/*.proto --python_out=.
RUN python setup.py build
RUN python setup.py install

WORKDIR /

COPY . /app
WORKDIR /app

CMD ["python", "main.py"]
