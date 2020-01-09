FROM python:3-alpine

RUN pip install awscli

RUN apk --no-cache add groff less

ENTRYPOINT [ "aws" ]
