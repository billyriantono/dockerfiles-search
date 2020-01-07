FROM google/cloud-sdk:alpine
ARG KLAR_URL="https://github.com/optiopay/klar/releases/download/v2.3.0/klar-2.3.0-linux-amd64"
USER root
# download klar for vulnarability scanning
RUN curl -L "$KLAR_URL" -o klar && \
    chmod +x klar && \
    mv klar /usr/local/bin
ENTRYPOINT ["/bin/bash", "-c"]
