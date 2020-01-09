FROM python:3.6-alpine

RUN apk --update add --no-cache bash build-base linux-headers pcre-dev libffi-dev libressl-dev automake gcc g++ subversion lsof uwsgi-python3 yarn git openssh-client

RUN mkdir /CashStory
WORKDIR /CashStory

COPY requirements.txt .

RUN pip3 install -r requirements.txt

CMD ["/bin/bash"]