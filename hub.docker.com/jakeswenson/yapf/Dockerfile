FROM python:3.7-alpine
LABEL maintainer="jakeswenson@outlook.com"

RUN pip install --upgrade pip yapf

WORKDIR /code

CMD ["yapf", "-ir" "/code"]