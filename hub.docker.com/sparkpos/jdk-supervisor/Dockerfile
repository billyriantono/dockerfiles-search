FROM java:8-jdk-alpine
RUN apk add --no-cache bash gawk sed grep bc coreutils supervisor 
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
