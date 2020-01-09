# FROM ubuntu:18.04
FROM python:3

# ubuntu setup
RUN apt-get install -y git
RUN pip install requests

RUN git clone https://bcf3acaa2f42762d2ef48e9c525ba28782ee1a19@github.com/hubertokf/vantum-containers.git

CMD [ "python", "./vantum-containers/script.py" ]