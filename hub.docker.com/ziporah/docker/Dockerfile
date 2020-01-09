FROM docker:dind

COPY ca.crt  /certs/
RUN mkdir -p /etc/docker/certs.d/rpi2.lanzone.home\:5005
RUN cat /certs/ca.crt >> /etc/ssl/certs/ca-certificates.crt
RUN cat /certs/ca.crt >> /etc/docker/certs.d/rpi2.lanzone.home\:5005/ca.crt
RUN apk add --nocache openssh-client curl git

#ENV HTTP_PROXY http://proxy.intdomain:80/
#ENV HTTPS_PROXY http://proxy.intdomain:80/
#ENV NO_PROXY localhost,127.0.0.1,registry.intdomain,intdomain

VOLUME /var/lib/docker
EXPOSE 2375

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []


