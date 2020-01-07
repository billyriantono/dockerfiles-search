FROM docker:git

COPY ./intrinsec /usr/share/ca-certificates/intrinsec/

RUN sh -c "echo intrinsec/Intrinsec-Internal-Root-Enterprise-CA-2019.pem >> /etc/ca-certificates.conf" && \
    sh -c "echo intrinsec/Intrinsec-Internal-Root-Enterprise-CA-2025.pem >> /etc/ca-certificates.conf" && \
    update-ca-certificates
