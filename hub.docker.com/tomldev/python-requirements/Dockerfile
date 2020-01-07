FROM python:3.7.1-alpine3.8

RUN mkdir -p /requirements

WORKDIR /requirements

RUN pip install pipreqs

COPY execute.sh execute.sh

ENTRYPOINT [ "./execute.sh" ]