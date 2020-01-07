FROM python:3-slim

WORKDIR /project

RUN pip install wagtail

ADD assets /assets

ADD bootstrap.sh /bootstrap.sh
RUN chmod 755 /bootstrap.sh

ENTRYPOINT [ "/bootstrap.sh" ]