FROM rancher/cli:v0.6.10

ADD *.pem /etc/ssl/certs/

RUN update-ca-certificates && \
    cat /etc/ssl/certs/dcg-intermediate.pem /etc/ssl/certs/dcg-root.pem \
    >> /etc/ssl/certs/ca-certificates.crt
