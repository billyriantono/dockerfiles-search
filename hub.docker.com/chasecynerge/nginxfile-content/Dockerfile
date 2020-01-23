FROM tensorflow/tensorflow:2.0.0-py3

RUN mkdir /app
WORKDIR /app

COPY ./requirements.txt /app/requirements.txt
COPY ./cifar10_cnn.py /app/cifar10_cnn.py

RUN chmod +x /app/cifar10_cnn.py

RUN pip3 install -r /app/requirements.txt

CMD tail -f /dev/null