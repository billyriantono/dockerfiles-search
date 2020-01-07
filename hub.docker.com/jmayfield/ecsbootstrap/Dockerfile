FROM alpine

RUN apk update && apk add curl groff less python py-pip nmap
RUN pip install awscli
RUN curl -s https://get.docker.com/builds/Linux/x86_64/docker-1.9.1 > \
    /usr/bin/docker && chmod +x /usr/bin/docker
COPY run /

CMD /run
