FROM traefik:latest

ADD custom-ca.pem /usr/local/share/ca-certificates/custom-ca
RUN ls -la /usr/local/share/ca-certificates && \
    update-ca-certificates
