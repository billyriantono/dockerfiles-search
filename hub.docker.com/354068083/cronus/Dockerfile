FROM python:3.6.8-alpine3.9
RUN adduser --disabled-password --gecos '' cronus
# USER cronus
RUN mkdir /backend
RUN mkdir -p /backend/logs
WORKDIR /backend/
RUN apk --no-cache --update add vim curl sshpass procps net-tools nginx
RUN apk --no-cache --update add --virtual .build-deps openssl-dev gcc libffi-dev libc-dev linux-headers
COPY requirements.txt /backend/requirements.txt
RUN pip3 install --upgrade pip && pip3 install -r /backend/requirements.txt \
    && apk del .build-deps;
COPY . /backend/
RUN touch /backend/logs/cronus.log
RUN chmod 777 /backend/logs/cronus.log

EXPOSE 8081
CMD ["/bin/sh", "run_django.sh"]
