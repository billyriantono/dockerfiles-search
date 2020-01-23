FROM alpine:3.10

RUN apk add --no-cache \
        uwsgi-python3 \
        uwsgi-http \
        uwsgi-router_http \
        python3 \
        py3-psycopg2

RUN pip3 install --no-cache-dir ara[server]==1.1.0

EXPOSE 8000

CMD [ "uwsgi", "--http-socket", "0.0.0.0:8000", \
               "--uid", "uwsgi", \
               "--plugins", "python3", \
               "--protocol", "uwsgi", \
               "--wsgi", "ara.server.wsgi" ]
