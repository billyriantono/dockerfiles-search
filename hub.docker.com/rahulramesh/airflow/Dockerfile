FROM ubuntu:18.04

RUN apt-get update && apt-get install -y python3 && apt-get install -y python3-dev && apt-get install -y python3-pip && apt-get install -y build-essential libssl-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev && apt-get clean

COPY python_reqs /tmp/
 
RUN pip3 install -r /tmp/python_reqs

