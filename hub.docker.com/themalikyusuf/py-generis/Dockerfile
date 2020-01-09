  
FROM python:rc-alpine

RUN apk update

COPY ./generate.py ./usr/local/bin/generate.py

RUN chmod 0755 /usr/local/bin/generate.py

ENTRYPOINT ["python", "./usr/local/bin/generate.py"]