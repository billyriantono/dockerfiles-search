FROM tensorflow/tensorflow:1.12.0-py3

ENV LANG=C.UTF-8
WORKDIR /TwitterBot
ADD . /TwitterBot

RUN pip3 install -r requirements.txt
RUN python3 src/download_model.py 117M

CMD python3 src/main.py
