FROM python:3-alpine3.9

RUN pip install -U --quiet elasticsearch-curator==5.8.1

ENTRYPOINT [ "/usr/local/bin/curator" ]
