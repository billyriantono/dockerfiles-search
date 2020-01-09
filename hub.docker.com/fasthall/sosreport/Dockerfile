FROM ubuntu:xenial

LABEL maintainer="weitsung@google.com,jiayingz@google.com"

RUN apt update -qq && apt install -y -qq git python python-pip
RUN git clone git://github.com/sosreport/sos.git

WORKDIR /sos
RUN pip install -r requirements.txt

CMD ["/bin/bash", "-c", "./sosreport -a --config ./sos.conf --batch --quiet"]
