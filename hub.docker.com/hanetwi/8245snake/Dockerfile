FROM python:3.7.3

WORKDIR /usr/src/app

ADD requirements.txt /usr/src/app/

RUN apt-get update
RUN pip install --upgrade pip

RUN pip install --extra-index-url=https://gergely.imreh.net/wheels/ numpy
RUN pip install --no-cache-dir -r requirements.txt


CMD ["/bin/bash"]
