FROM jfloff/alpine-python:2.7-slim

LABEL maintainer=buurman
WORKDIR /opt/autosub-master

RUN apk update && \
    apk add \
       gcc \
        python-dev \
        musl-dev && \
   wget https://github.com/BenjV/autosub/archive/master.zip && \
   unzip master.zip -d /opt && \
   rm master.zip && \
   easy_install Cheetah

CMD [ "python", "AutoSub.py" ]
EXPOSE 9960
