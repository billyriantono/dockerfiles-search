FROM identt/rancher-compose:0.12.5

ADD *.pem /etc/ssl/certs/

RUN update-ca-certificates && \
    cat /etc/ssl/certs/dcg-intermediate.pem /etc/ssl/certs/dcg-root.pem \
    >> /etc/ssl/certs/ca-certificates.crt
