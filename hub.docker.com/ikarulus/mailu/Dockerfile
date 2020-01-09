FROM alpine:edge

RUN apk add --no-cache nginx nginx-mod-mail python py-jinja2 certbot libressl

COPY conf /conf
COPY *.py /

CMD /start.py
