# FROM python:2-alpine ### pip install build failures with the likes of lxml
FROM python:2

#RUN apk add --update --no-cache alpine-sdk bash gawk sed grep bc coreutils git

## Install odpdown
RUN cd / && git clone https://github.com/thorstenb/odpdown.git
RUN cd /odpdown \
  && pip install -r requirements.txt \
  && python setup.py install

RUN mkdir /convert
VOLUME /convert
WORKDIR /convert

CMD [ "python", "odpdown" ]