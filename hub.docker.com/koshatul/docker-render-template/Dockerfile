FROM alpine:3.7
RUN apk add --no-cache python py-jinja2

COPY init.py /init.py
ENTRYPOINT [ "/init.py" ]
