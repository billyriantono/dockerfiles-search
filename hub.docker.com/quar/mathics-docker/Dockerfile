FROM python:alpine3.7

RUN pip install mathics

EXPOSE 8000

ENTRYPOINT ["/usr/bin/env", "mathicsserver", "--external"]
