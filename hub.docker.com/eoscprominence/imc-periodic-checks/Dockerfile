FROM alpine:latest
RUN apk add --no-cache gcc \
                       musl-dev \
                       linux-headers \
                       uwsgi-python \
                       uwsgi-http \
                       python \
                       python-dev \
                       py-requests \ 
                       py-flask \
                       py-futures \
                       py-paramiko \
                       py-psycopg2 \
                       py-pip && \
    pip install apache-libcloud && \
    pip install python-openstackclient


COPY imc /imc

RUN chown uwsgi /var/log && \
    mkdir /var/lib/prominence && \
    chown uwsgi /var/lib/prominence

USER uwsgi

ENTRYPOINT ["python", "/imc/periodic-checks.py"]
