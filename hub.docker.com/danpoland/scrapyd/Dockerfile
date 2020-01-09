FROM python:2.7
MAINTAINER Daniel Poland <danpoland84@gmail.com>

RUN pip install scrapyd requests
RUN mkdir -p /etc/scrapyd

COPY ./scrapyd.conf /etc/scrapyd/

EXPOSE 6800

CMD ["scrapyd"]