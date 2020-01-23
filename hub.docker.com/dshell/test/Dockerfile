FROM busybox:latest
MAINTAINER john<zhxiaog@outlook.com>

RUN mkdir -p /var/dshell
RUN echo OK > /var/dshell/health

EXPOSE 8080

ENTRYPOINT ["httpd","-p", "8080", "-h", "/var/dshell", "-f"]