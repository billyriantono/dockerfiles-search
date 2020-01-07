FROM python:3.7.2-alpine

RUN apk update && apk add build-base

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt                     && \
    rm requirements.txt                                 && \
    adduser -DH pkpic2gcalendar                         && \
    mkdir /var/secret                                   && \
    chown pkpic2gcalendar:pkpic2gcalendar /var/secret
VOLUME /var/secret

WORKDIR /usr/local/bin/
COPY src .

USER pkpic2gcalendar

ENV P2G_SECRET_PATH=/var/secret

ENTRYPOINT ["./pkpic2gcalendar.py"]
CMD ["start", "--poll-for-auth"]
