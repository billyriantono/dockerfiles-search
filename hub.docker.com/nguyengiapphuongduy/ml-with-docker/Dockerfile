FROM ubuntu:18.04

WORKDIR /mlapp

ADD . /mlapp


RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends python3.7-minimal python3-pip python3-setuptools

RUN rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir -r with-dependencies.txt
RUN pip3 install --no-cache-dir --no-dependencies -r no-dependencies.txt


ENTRYPOINT [ "python3" ]

CMD [ "main.py" ]
