FROM mcr.microsoft.com/powershell:6.2.2-alpine-3.8
LABEL maintainer="rxbn"
COPY Update-CloudflareDNS.ps1 /app/Update-CloudflareDNS.ps1
COPY docker/init.sh /
RUN apk add --update curl && \
    rm -rf /var/cache/apk/* && \
    chmod +x /init.sh
VOLUME ["/opt/config"]
ENTRYPOINT ["/init.sh"]