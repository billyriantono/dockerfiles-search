FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:deadsnakes/ppa -y
RUN apt-get install python3-pip python3-dev -y 
RUN pip3 install --upgrade pip 
RUN pip install jupyter

RUN mkdir -p /src

WORKDIR /src/

ADD . /src/
RUN pip install -r requirements.txt

CMD jupyter notebook --allow-root --ip='0.0.0.0'
