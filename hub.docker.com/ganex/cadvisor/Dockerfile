FROM google/cadvisor:v0.25.0
MAINTAINER Ganex <suporte@ganex.com.br>

# Timezone
RUN apk add --update tzdata && cp /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

# Update findutils
RUN apk add --update findutils && rm -rf /var/cache/apk/*

