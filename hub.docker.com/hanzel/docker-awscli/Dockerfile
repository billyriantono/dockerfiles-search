FROM docker:git

RUN apk update && apk add python
RUN wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install awscli
