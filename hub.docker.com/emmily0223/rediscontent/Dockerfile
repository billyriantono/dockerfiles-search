FROM docker:stable

RUN apk add py-pip
RUN apk add python-dev libffi-dev openssl-dev gcc libc-dev make
RUN pip install docker-compose

CMD ["docker-compose", "-v"]
