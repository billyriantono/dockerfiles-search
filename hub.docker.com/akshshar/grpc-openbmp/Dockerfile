FROM akshshar/confluent-python

RUN apt-get update && apt-get install -y git vim python-dev python-pip libsnappy-dev

RUN pip install kafka-python pyyaml six py2-ipaddress grpcio

RUN git clone https://github.com/OpenBMP/openbmp-python-api-message.git /openbmp

RUN pip install /openbmp
