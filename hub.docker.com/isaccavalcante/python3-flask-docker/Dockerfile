FROM python:3.6.2
MAINTAINER Isac C. "isaccavalcante@alu.ufc.br"

ADD requirements.txt .

RUN pip3 install --upgrade pip && pip3 install -r requirements.txt 

RUN apt-get update && \
    apt-get install -y locales

RUN locale-gen pt_BR.UTF-8 \
    && update-locale 

ENV LANG pt_BR.UTF-8