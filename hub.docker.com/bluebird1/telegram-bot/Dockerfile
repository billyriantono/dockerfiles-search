FROM python:3.6.7-alpine3.7
LABEL maintainer="linlanxi7552659@gmail.com"
WORKDIR /opt/bot
ONBUILD  COPY . /opt/bot
ONBUILD RUN  apk --no-cache --virtual build  add build-base libffi-dev openssl-dev && pip install -r requirements.txt && rm -rf ~/.pip/ && apk del build 
ONBUILD CMD ["python","run.py"]

