FROM python:alpine
RUN pip install awscli
RUN apk add --no-cache groff less
RUN mkdir /code
WORKDIR /code
ENTRYPOINT [ "aws" ]

